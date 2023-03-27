# Builder Design Pattern

## 1. Pattern Name
Builder

## 2. Problem
The Builder pattern addresses the problem of constructing complex objects with multiple configurations or variations. It is particularly useful when the process of constructing an object involves a large number of steps, or when the object's construction requires a specific order of operations.

## 3. Solution
The Builder pattern suggests separating the construction of an object from its representation. This separation is achieved by creating a `Builder` interface, which specifies the steps required to build the object, and one or more `ConcreteBuilder` classes, which implement the interface and provide the actual construction logic. The `Director` class is responsible for controlling the order of the construction process and assembling the final product.

## 4. Consequences
- Separation of construction and representation makes it easier to manage the construction process and extend the system with new configurations.
- Improved code maintainability and readability by encapsulating the construction logic in dedicated builder classes.
- The Builder pattern allows for better control over the object construction process.

However, the pattern can lead to increased code complexity due to the introduction of additional classes and interfaces.

## 5. Implementation
Here's an example implementation of the Builder pattern in Python:

```python
from abc import ABC, abstractmethod

class Director:
    def __init__(self, builder):
        self._builder = builder

    def construct(self):
        self._builder.build_part_a()
        self._builder.build_part_b()
        self._builder.build_part_c()
        return self._builder.get_result()

class Builder(ABC):
    @abstractmethod
    def build_part_a(self):
        pass

    @abstractmethod
    def build_part_b(self):
        pass

    @abstractmethod
    def build_part_c(self):
        pass

    @abstractmethod
    def get_result(self):
        pass

class ConcreteBuilder(Builder):
    def __init__(self):
        self._product = Product()

    def build_part_a(self):
        self._product.add("Part A")

    def build_part_b(self):
        self._product.add("Part B")

    def build_part_c(self):
        self._product.add("Part C")

    def get_result(self):
        return self._product

class Product:
    def __init__(self):
        self._parts = []

    def add(self, part):
        self._parts.append(part)

    def display(self):
        print("Product parts:", self._parts)

# Client code
builder = ConcreteBuilder()
director = Director(builder)
product = director.construct()
product.display()

```

6. Participants
Director: Controls the object construction process.
Builder: The abstract interface for creating objects (parts of the product).
ConcreteBuilder: Provides a specific implementation of the Builder interface.
Product: Represents the complex object being built.

7. Collaborations
The Director controls the construction process by calling the appropriate methods on the Builder interface.
The ConcreteBuilder implements the Builder interface, providing the actual construction logic.
The Product class represents the complex object that results from the construction process.

8. Real-world examples
Building complex documents with different formats (e.g., HTML, PDF, or plain text) while maintaining a consistent structure.
Constructing UI components that have various configurations or styles.
