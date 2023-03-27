## Command Design Pattern

### Pattern Name
Command

### Problem
There's a need to decouple the object that invokes an action (called the invoker) from the object that performs the action (called the receiver). This enables more flexibility in managing actions, making them easily extensible, interchangeable, and simplifying the invoker's implementation.

### Solution
The Command pattern proposes encapsulating actions in separate objects called "commands." These command objects have a common interface, typically with an `execute()` method. The invoker holds references to command objects and delegates the execution of actions to them. By doing so, the invoker doesn't need to know the specifics of how an action is performed or which receiver is involved.

### Consequences
**Benefits:**
- Decouples the invoker from the receiver, promoting loose coupling and separation of concerns.
- Simplifies the invoker's implementation, as it doesn't need to know about the specifics of each action.
- Allows easy extension and addition of new commands without modifying the invoker.
- Supports undo and redo operations if the commands store their state before execution.

**Drawbacks:**
- Can lead to an increased number of classes and objects for simple actions, potentially adding complexity.

### Implementation
Here's an example of the Command pattern in Python:

```python
from abc import ABC, abstractmethod

class Command(ABC):
    @abstractmethod
    def execute(self):
        pass

class Light:
    def on(self):
        print("The light is on.")

    def off(self):
        print("The light is off.")

class LightOnCommand(Command):
    def __init__(self, light):
        self._light = light

    def execute(self):
        self._light.on()

class LightOffCommand(Command):
    def __init__(self, light):
        self._light = light

    def execute(self):
        self._light.off()

class RemoteControl:
    def __init__(self):
        self._command = None

    def set_command(self, command):
        self._command = command

    def press_button(self):
        self._command.execute()

# Client code
light = Light()
light_on = LightOnCommand(light)
light_off = LightOffCommand(light)

remote = RemoteControl()

remote.set_command(light_on)
remote.press_button()

remote.set_command(light_off)
remote.press_button()

```

Participants
Command: The command interface that declares the execute() method.
LightOnCommand and LightOffCommand: Concrete command classes that implement the Command interface and perform specific actions on the receiver.
Light: The receiver class that performs the actual actions (in this case, turning the light on or off).
RemoteControl: The invoker class that holds a reference to a command object and delegates the execution of the action to the command.

Collaborations
The invoker (RemoteControl) holds a reference to a command object and calls its execute() method when required.
Concrete command classes (LightOnCommand and LightOffCommand) implement the Command interface and define the specific action to perform on the receiver.
The receiver (Light) is the object that performs the actual action.

Real-world examples
GUI buttons and menu items, where each button or menu item represents a command and the GUI framework acts as the invoker.
Task schedulers and job queues that execute commands at specific times or under certain conditions.
Macro recording systems, where a series of commands are recorded and executed in sequence.
