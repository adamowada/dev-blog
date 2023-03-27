# Visitor Design Pattern

## 1. Pattern Name
Visitor

## 2. Problem
When you have a complex object structure (e.g., a composite structure), and you need to perform operations on these objects that depend on their concrete classes, but you want to avoid adding new methods to the classes for each new operation.

## 3. Solution
The Visitor pattern suggests that you place the new operation into a separate class called a visitor, instead of adding methods to existing classes. Then, you can pass the visitor object to the elements of the structure, allowing the elements to "accept" the visitor and "let it in." The visitor can then access the elements' state and perform the operation.

## 4. Consequences
Benefits:
- Separation of concerns: The visitor pattern separates the algorithm from the object structure, making it easier to add new operations.
- Open/Closed Principle: Object structures can be extended with new elements without changing the existing operations.

Drawbacks:
- Dependency: The visitor pattern introduces a new dependency between the visitor classes and the element classes.
- Violates encapsulation: The pattern often requires exposing the internal state and behavior of the elements, which can be seen as violating the encapsulation principle.

## 5. Implementation
Here's a basic example of the Visitor pattern in Python:

```python
from abc import ABC, abstractmethod

class Element(ABC):
    @abstractmethod
    def accept(self, visitor):
        pass

class ConcreteElementA(Element):
    def accept(self, visitor):
        visitor.visit_concrete_element_a(self)

    def operation_a(self):
        return "ConcreteElementA operation"

class ConcreteElementB(Element):
    def accept(self, visitor):
        visitor.visit_concrete_element_b(self)

    def operation_b(self):
        return "ConcreteElementB operation"

class Visitor(ABC):
    @abstractmethod
    def visit_concrete_element_a(self, element):
        pass

    @abstractmethod
    def visit_concrete_element_b(self, element):
        pass

class ConcreteVisitor1(Visitor):
    def visit_concrete_element_a(self, element):
        print(f"ConcreteVisitor1: {element.operation_a()}")

    def visit_concrete_element_b(self, element):
        print(f"ConcreteVisitor1: {element.operation_b()}")

class ConcreteVisitor2(Visitor):
    def visit_concrete_element_a(self, element):
        print(f"ConcreteVisitor2: {element.operation_a()}")

    def visit_concrete_element_b(self, element):
        print(f"ConcreteVisitor2: {element.operation_b()}")

# Client code
element_a = ConcreteElementA()
element_b = ConcreteElementB()

visitor1 = ConcreteVisitor1()
visitor2 = ConcreteVisitor2()

element_a.accept(visitor1)
element_a.accept(visitor2)
element_b.accept(visitor1)
element_b.accept(visitor2)

```

6. Participants
Element: An interface for the elements that defines the accept method.
ConcreteElementA and ConcreteElementB: Concrete classes that implement the Element interface.
Visitor: An interface for the visitors, with methods for each type of concrete element.
ConcreteVisitor1 and ConcreteVisitor2: Concrete visitor classes that implement the Visitor interface, each providing a specific operation.

7. Collaborations
The Element interface defines an accept method that takes a Visitor as an argument. The concrete elements implement this method and let the visitor access their state and behavior.
The Visitor interface defines the methods for each concrete element. The concrete visitors implement these methods and provide the specific operations or algorithms to be executed on the concrete elements.

8. Real-world examples
Parsing and processing an Abstract Syntax Tree (AST) in a compiler or interpreter. Different visitors can be implemented for tasks such as type checking, code optimization, and code generation.
Rendering graphical objects in a graphical user interface (GUI). Different visitors can be implemented to render objects in different formats or styles, without modifying the graphical object classes.
Here's the complete Python example code:

```python
from abc import ABC, abstractmethod

class Element(ABC):
    @abstractmethod
    def accept(self, visitor):
        pass

class ConcreteElementA(Element):
    def accept(self, visitor):
        visitor.visit_concrete_element_a(self)

    def operation_a(self):
        return "ConcreteElementA operation"

class ConcreteElementB(Element):
    def accept(self, visitor):
        visitor.visit_concrete_element_b(self)

    def operation_b(self):
        return "ConcreteElementB operation"

class Visitor(ABC):
    @abstractmethod
    def visit_concrete_element_a(self, element):
        pass

    @abstractmethod
    def visit_concrete_element_b(self, element):
        pass

class ConcreteVisitor1(Visitor):
    def visit_concrete_element_a(self, element):
        print(f"ConcreteVisitor1: {element.operation_a()}")

    def visit_concrete_element_b(self, element):
        print(f"ConcreteVisitor1: {element.operation_b()}")

class ConcreteVisitor2(Visitor):
    def visit_concrete_element_a(self, element):
        print(f"ConcreteVisitor2: {element.operation_a()}")

    def visit_concrete_element_b(self, element):
        print(f"ConcreteVisitor2: {element.operation_b()}")

# Client code
element_a = ConcreteElementA()
element_b = ConcreteElementB()

visitor1 = ConcreteVisitor1()
visitor2 = ConcreteVisitor2()

element_a.accept(visitor1)
element_a.accept(visitor2)
element_b.accept(visitor1)
element_b.accept(visitor2)

```

This example demonstrates the Visitor design pattern in Python, with concrete elements, concrete visitors, and the interactions between them.
