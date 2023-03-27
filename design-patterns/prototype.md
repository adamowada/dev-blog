1. Pattern Name
---------------
Prototype

2. Problem
----------
The need to create new objects that are a copy or a variation of an existing object, especially when object creation is resource-intensive or requires complex initialization.

3. Solution
-----------
The Prototype pattern involves cloning an existing object (the prototype) instead of creating a new one from scratch. This pattern relies on the object's ability to create a copy of itself, which is then modified as needed.

4. Consequences
---------------
Benefits:
- Faster object creation, especially when instantiation is expensive or complex.
- Greater flexibility in creating objects with varying state and behavior.
- Encapsulation of object creation details.

Drawbacks:
- Additional complexity introduced by the cloning process.
- Difficulty in handling objects with circular references or complex internal structures.

5. Implementation
-----------------
In Python, the `copy` module can be used to implement cloning. The module provides methods like `copy()` and `deepcopy()` to create shallow and deep copies of objects, respectively.

6. Participants
----------------
- Prototype: An interface or an abstract class defining the cloning method.
- ConcretePrototype: A class implementing the Prototype interface or inheriting from the abstract class, providing an implementation of the cloning method.

7. Collaborations
-----------------
The client requests a new object from the ConcretePrototype by invoking the cloning method. The ConcretePrototype creates a copy of itself and returns it to the client.

8. Real-world examples
-----------------------
- Creating new instances of GUI elements with the same style and properties.
- Instantiating game characters with different attributes based on a template.

Example Python code:

```python
import copy

class Prototype:
    def clone(self):
        raise NotImplementedError("Subclasses should implement the 'clone' method.")

class ConcretePrototype(Prototype):
    def __init__(self, attribute):
        self.attribute = attribute

    def clone(self):
        return copy.deepcopy(self)

# Client code
prototype = ConcretePrototype("original attribute")
print(prototype.attribute)  # Output: original attribute

cloned_object = prototype.clone()
cloned_object.attribute = "modified attribute"
print(cloned_object.attribute)  # Output: modified attribute
print(prototype.attribute)  # Output: original attribute (remains unchanged)

```
