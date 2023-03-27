1. Pattern Name: Memento

2. Problem: 
The Memento pattern addresses the need to restore an object to a previous state without exposing its internal details. It is particularly useful when you want to implement undo or rollback functionality for an object without violating the encapsulation principle.

3. Solution: 
The Memento pattern involves three participants: the Originator, the Caretaker, and the Memento. The Originator creates a Memento object, which stores its internal state. The Caretaker is responsible for managing the Memento and can request the Originator to save or restore its state using the Memento.

4. Consequences: 

- Benefits:
    - Encapsulates the state-saving and restoration logic, ensuring the internal state of the Originator remains hidden.
    - Allows multiple checkpoints, making it possible to revert to different previous states.

- Drawbacks:
    - May consume more memory, as it requires storing multiple Memento objects for different states.
    - Increases complexity due to the additional classes and interactions.

5. Implementation:
In Python, you can implement the Memento pattern using classes for the Originator, Memento, and Caretaker. You can use Python's built-in `__dict__` attribute to store and restore the object's state.

6. Participants:
- Originator: The object whose state needs to be saved and restored.
- Memento: The object that stores the internal state of the Originator.
- Caretaker: The object that is responsible for the Memento's safekeeping and managing the state restoration process.

7. Collaborations:
- The Caretaker requests the Originator to create a Memento.
- The Originator creates a Memento with its current state.
- The Caretaker stores the Memento.
- When required, the Caretaker requests the Originator to restore its state from a specific Memento.

8. Real-world examples:
- Implementing undo functionality in text editors or image editing software.
- Maintaining the history of different versions of an object in a version control system.

Example Code:

```python
class Memento:
    def __init__(self, state):
        self._state = state

    def get_state(self):
        return self._state


class Originator:
    _state = ""

    def set_state(self, state):
        self._state = state

    def create_memento(self):
        return Memento(self._state)

    def restore_state(self, memento):
        self._state = memento.get_state()


class Caretaker:
    def __init__(self):
        self._mementos = []

    def add_memento(self, memento):
        self._mementos.append(memento)

    def get_memento(self, index):
        return self._mementos[index]


originator = Originator()
caretaker = Caretaker()

originator.set_state("State1")
caretaker.add_memento(originator.create_memento())

originator.set_state("State2")
caretaker.add_memento(originator.create_memento())

originator.set_state("State3")
caretaker.add_memento(originator.create_memento())

originator.restore_state(caretaker.get_memento(0))
print(originator._state)  # Output: State1

originator.restore_state(caretaker.get_memento(1))
print(originator._state)  # Output: State2

```
