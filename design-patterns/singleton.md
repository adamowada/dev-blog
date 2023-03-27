Pattern Name: Singleton
The Singleton pattern ensures that a class has only one instance and provides a global point of access to that instance.

Problem:
The problem arises when a class should only have one instance, which can be accessed globally throughout the application. This can be useful for managing resources like database connections or application configurations, where having multiple instances would lead to inconsistencies and increased resource usage.

Solution:
The Singleton pattern suggests creating a class that can only be instantiated once, and providing a method to access that single instance whenever needed. This is achieved by making the constructor private or protected, and creating a static method to manage the instance creation and access.

Consequences:
Benefits:

Ensures a single instance of a class, preventing duplicate resources or inconsistent states.
Provides a global point of access to the instance, simplifying resource management.
Drawbacks:

Singleton instances can become a source of global mutable state, which may introduce issues in a multi-threaded environment.
Can make unit testing more challenging due to the global nature of the pattern.
Implementation:
In Python, the Singleton pattern can be implemented using various techniques such as class decorators, metaclasses, or by overriding the __new__ method. Here's an example using the __new__ method:

```python
Copy code
class Singleton:
    _instance = None

    def __new__(cls, *args, **kwargs):
        if cls._instance is None:
            cls._instance = super().__new__(cls, *args, **kwargs)
        return cls._instance

    def __init__(self):
        self.some_attribute = "Singleton attribute"

# Usage
singleton1 = Singleton()
singleton2 = Singleton()

print(singleton1 is singleton2)  # Output: True

```

Participants:
Singleton: The class implementing the Singleton pattern, with a private or protected constructor, and a method to access the single instance.
Collaborations:
The Singleton class collaborates with itself to ensure that only one instance of the class is created and accessible through the designated method.

Real-world examples:
Logging frameworks, where a single instance is responsible for handling logs throughout the application.
Configuration managers, which maintain a single set of application-wide settings.
Database connection pools, where a single instance manages and distributes connections to avoid excessive resource usage.
