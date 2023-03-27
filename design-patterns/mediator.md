# Mediator Design Pattern

## 1. Pattern Name
Mediator

## 2. Problem
When you have multiple objects that need to communicate or interact with each other, managing their relationships can become complex and difficult to maintain. This can lead to high coupling between components, making the system harder to understand and modify.

## 3. Solution
The Mediator pattern introduces a central object, called the mediator, that encapsulates and coordinates the interactions between different objects. This allows for the decoupling of the components and reduces their dependencies on each other.

## 4. Consequences
- Pros:
  - Reduces coupling between components, making the system easier to understand and maintain.
  - Simplifies communication between objects, as they only need to interact with the mediator.
  - Enhances modularity and flexibility of the system.

- Cons:
  - The mediator can become a single point of failure or a bottleneck if not implemented properly.
  - The mediator itself can become overly complex as it handles interactions for multiple components.

## 5. Implementation

```python
from abc import ABC, abstractmethod


class Mediator(ABC):
    @abstractmethod
    def notify(self, sender, event):
        pass


class ConcreteMediator(Mediator):
    def __init__(self):
        self.colleague1 = None
        self.colleague2 = None

    def notify(self, sender, event):
        if sender == self.colleague1:
            self.colleague2.react_to_event(event)
        else:
            self.colleague1.react_to_event(event)


class Colleague(ABC):
    def __init__(self, mediator: Mediator):
        self.mediator = mediator

    @abstractmethod
    def react_to_event(self, event):
        pass


class Colleague1(Colleague):
    def trigger_event(self, event):
        self.mediator.notify(self, event)

    def react_to_event(self, event):
        print(f"Colleague1 reacting to event: {event}")


class Colleague2(Colleague):
    def trigger_event(self, event):
        self.mediator.notify(self, event)

    def react_to_event(self, event):
        print(f"Colleague2 reacting to event: {event}")


def main():
    mediator = ConcreteMediator()

    colleague1 = Colleague1(mediator)
    colleague2 = Colleague2(mediator)

    mediator.colleague1 = colleague1
    mediator.colleague2 = colleague2

    colleague1.trigger_event("Event from Colleague1")
    colleague2.trigger_event("Event from Colleague2")


if __name__ == "__main__":
    main()

```

6. Participants
Mediator (interface): Defines the interface for communication between Colleague objects.
ConcreteMediator: Implements the Mediator interface and coordinates communication between Colleague objects.
Colleague (interface): Defines the interface for objects that communicate through the Mediator.
Concrete Colleagues (Colleague1 and Colleague2): Implement the Colleague interface and interact with other colleagues through the Mediator.

7. Collaborations
Concrete Colleagues communicate with each other through the Mediator. When a Colleague triggers an event, it informs the Mediator, which then coordinates the appropriate response with the other Colleagues.

8. Real-world examples
Chat applications where the server acts as a mediator between different clients.
Model-View-Controller (MVC) architectural pattern, where the controller mediates between the model and the view components.
