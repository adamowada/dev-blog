1. Pattern Name: Bridge

2. Problem:
The Bridge pattern addresses the problem of separating an abstraction from its implementation so that both can evolve independently. This is particularly useful when you want to avoid tight coupling between components and provide flexibility for extension.

3. Solution:
The Bridge pattern achieves this separation by introducing an intermediate abstraction layer that acts as a bridge between the high-level abstraction and its concrete implementation. The abstraction layer contains a reference to the implementation, which can be changed at runtime. This allows for greater flexibility and the ability to switch implementations without modifying the abstraction.

4. Consequences:
   Benefits:
   - Decouples the abstraction from its implementation, allowing both to evolve independently.
   - Improves code maintainability and readability by separating concerns.
   - Allows for easier extension and modification of implementations.

   Drawbacks:
   - Adds complexity to the code, especially when the problem it solves is not very significant.

5. Implementation:
To implement the Bridge pattern in Python, you will create an abstract base class for the abstraction layer and an abstract base class for the implementation layer. Concrete classes will inherit from these abstract classes to provide specific functionality.

6. Participants:
   - Abstraction: Defines the high-level abstraction interface and contains a reference to the implementation.
   - RefinedAbstraction: Extends the Abstraction to provide more specific functionality.
   - Implementor: The abstract base class for the implementation layer.
   - ConcreteImplementor: A concrete class that inherits from Implementor and provides a specific implementation.

7. Collaborations:
The Abstraction collaborates with the Implementor by delegating some of its responsibilities to the Implementor. Clients use the RefinedAbstraction and can switch between different ConcreteImplementors without affecting the abstraction's usage.

8. Real-world examples:
   - Platform-independent GUI frameworks, where the same UI components can be used on different platforms (e.g., Windows, macOS, Linux) with platform-specific implementations.
   - Different database drivers providing a unified interface to access various databases.

Example Code:

```python
from abc import ABC, abstractmethod

# Implementor
class DrawingAPI(ABC):
    @abstractmethod
    def draw_circle(self, x, y, radius):
        pass

# ConcreteImplementor 1
class DrawingAPI1(DrawingAPI):
    def draw_circle(self, x, y, radius):
        print(f"API1.circle at {x}:{y} - radius {radius}")

# ConcreteImplementor 2
class DrawingAPI2(DrawingAPI):
    def draw_circle(self, x, y, radius):
        print(f"API2.circle at {x}:{y} - radius {radius}")

# Abstraction
class Shape(ABC):
    def __init__(self, drawing_api: DrawingAPI):
        self._drawing_api = drawing_api

    @abstractmethod
    def draw(self):
        pass

    @abstractmethod
    def resize_by_percentage(self, percent):
        pass

# RefinedAbstraction
class CircleShape(Shape):
    def __init__(self, x, y, radius, drawing_api: DrawingAPI):
        super().__init__(drawing_api)
        self._x = x
        self._y = y
        self._radius = radius

    def draw(self):
        self._drawing_api.draw_circle(self._x, self._y, self._radius)

    def resize_by_percentage(self, percent):
        self._radius *= (1 + percent/100)

# Client
def main():
    shapes = [
        CircleShape(1, 2, 3, DrawingAPI1()),
        CircleShape(5, 7, 11, DrawingAPI2())
    ]

    for shape in shapes:
         shape.draw()
         shape.resize_by_percentage(50)
         shape.draw()
    
if name == "main":
    main()

```


In this example, the `DrawingAPI` serves as the Implementor, with `DrawingAPI1` and `DrawingAPI2` as the ConcreteImplementors. The `Shape` class is the Abstraction, and `CircleShape` is the RefinedAbstraction. Clients can use `CircleShape` with different drawing APIs, such as `DrawingAPI1` and `DrawingAPI2`, without modifying the code for `CircleShape`.
