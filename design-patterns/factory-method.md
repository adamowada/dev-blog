# Factory Method
<!-- attribution: created with ChatGPT/GPT-4 -->

## Problem 

The problem that the Factory Method pattern addresses is the creation of objects without specifying the exact class of the object that will be created. This is particularly useful when dealing with a family of related classes or when the exact class to be instantiated may change or depend on runtime conditions.

## Solution

The Factory Method pattern defines an interface or abstract class with a factory method for creating objects. Subclasses of this interface or abstract class override the factory method to create and return instances of different classes. The client code interacts with the interface or abstract class, delegating the responsibility of object creation to the factory method.

## Consequences

- Benefits:
  - Decouples the client code from the specific classes being instantiated.
  - Allows for easier introduction of new classes or modifications to existing classes.
  - Encourages adherence to the Open/Closed Principle, as new classes can be introduced without modifying the client code.

- Drawbacks:
  - May introduce extra complexity when only a simple object creation is needed.

## Implementation

Here's an example of the Factory Method pattern implemented in Python:

```python
from abc import ABC, abstractmethod


class Creator(ABC):
    @abstractmethod
    def factory_method(self):
        pass

    def some_operation(self):
        product = self.factory_method()
        return f"Creator: The same creator's code has just worked with {product.operation()}"


class ConcreteCreator1(Creator):
    def factory_method(self):
        return ConcreteProduct1()


class ConcreteCreator2(Creator):
    def factory_method(self):
        return ConcreteProduct2()


class Product(ABC):
    @abstractmethod
    def operation(self) -> str:
        pass


class ConcreteProduct1(Product):
    def operation(self) -> str:
        return "ConcreteProduct1"


class ConcreteProduct2(Product):
    def operation(self) -> str:
        return "ConcreteProduct2"


def client_code(creator: Creator) -> None:
    print(creator.some_operation(), end="\n")


if __name__ == "__main__":
    client_code(ConcreteCreator1())
    client_code(ConcreteCreator2())

```

## Participants:

- Creator (Abstract class): Declares the factory method and contains some operation that relies on the product returned by the factory method.
- ConcreteCreator1, ConcreteCreator2 (Concrete classes): Subclasses of the Creator that override the factory method to instantiate specific products.
- Product (Abstract class or interface): Defines the interface for the objects the factory method creates.
- ConcreteProduct1, ConcreteProduct2 (Concrete classes): Implement the Product interface and define the specific behavior of the products created by the corresponding ConcreteCreator.

## Collaborations: 

Client code calls the some_operation() method on a Creator object, which in turn calls the factory method. The factory method, implemented in the ConcreteCreator, creates and returns a ConcreteProduct object. The Creator then works with the Product object through its interface, without knowing the exact class of the object.

## Real-world examples:

A real-world example of the Factory Method pattern can be found in the Django web framework. Django uses the pattern to create form fields, database fields, and widgets, among other components, allowing for easy customization and extension.
