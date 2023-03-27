# State Design Pattern

## 1. Pattern Name
State

## 2. Problem
Managing state transitions and behavior changes in an object based on its internal state can lead to complex and tightly coupled code.

## 3. Solution
The State pattern allows an object to alter its behavior when its internal state changes. It does this by encapsulating state-specific behavior into separate state classes and delegating state transitions and behavior to these classes.

## 4. Consequences
Benefits:
- Encapsulates state-specific behavior, promoting separation of concerns.
- Simplifies code by avoiding large conditional statements or switch statements.
- Supports adding new states easily without modifying existing code.

Drawbacks:
- Can increase the number of classes in the system.

## 5. Implementation
In Python, the State pattern can be implemented using classes for each state and an interface or abstract class for the state objects to adhere to. The context class delegates state-specific behavior to state objects.

## 6. Participants
- Context: Defines the interface of interest to clients and maintains a reference to the current state object.
- State: An interface or abstract class that defines a common interface for all concrete state classes.
- ConcreteState: One or more classes implementing the State interface, each representing a specific state and its associated behavior.

## 7. Collaborations
The Context class delegates state-specific behavior to the current state object. When a state transition occurs, the Context replaces the current state object with a new one representing the next state.

## 8. Real-world examples
- Implementing a finite state machine for a game character that can be idle, walking, running, or jumping.
- Managing the state of a network connection (e.g., connected, disconnected, reconnecting).

# Example Code

```python
from abc import ABC, abstractmethod

class State(ABC):
    @abstractmethod
    def handle(self, context):
        pass

class ConcreteStateA(State):
    def handle(self, context):
        print("State A handling request")
        context.state = ConcreteStateB()

class ConcreteStateB(State):
    def handle(self, context):
        print("State B handling request")
        context.state = ConcreteStateA()

class Context:
    def __init__(self, state: State):
        self._state = state

    @property
    def state(self):
        return self._state

    @state.setter
    def state(self, state: State):
        self._state = state

    def request(self):
        self._state.handle(self)

# Client code
context = Context(ConcreteStateA())

context.request()
context.request()
context.request()

```
