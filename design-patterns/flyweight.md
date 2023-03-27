1. Pattern Name
---------------
Flyweight

2. Problem
----------
The Flyweight pattern is used when you need to create a large number of similar objects, but you want to minimize memory usage and improve performance. This problem arises when objects consume a significant amount of memory and could lead to resource constraints or slow performance.

3. Solution
-----------
The Flyweight pattern suggests separating the intrinsic (shared) and extrinsic (unique) state of an object. The intrinsic state is stored in a shared flyweight object, and the extrinsic state is passed to methods as arguments. This approach allows you to reuse the shared state and reduce memory overhead.

4. Consequences
---------------
Benefits:
- Reduced memory usage.
- Improved performance.
- Encourages object reuse.

Drawbacks:
- Increased complexity due to separating intrinsic and extrinsic states.
- The need for proper management of shared objects.

5. Implementation
-----------------
In Python, the Flyweight pattern can be implemented using a factory class to manage the creation and sharing of flyweight objects. This class can use a dictionary to store the shared flyweight objects based on a key.

6. Participants
----------------
- Flyweight (abstract class): Defines an interface for flyweight objects.
- ConcreteFlyweight (class): Implements the Flyweight interface and stores the intrinsic state.
- FlyweightFactory (class): Manages the creation and sharing of flyweight objects.
- Client: Interacts with the FlyweightFactory to get flyweight objects and operates on their extrinsic state.

7. Collaborations
-----------------
- The Client requests a flyweight object from the FlyweightFactory.
- The FlyweightFactory returns an existing ConcreteFlyweight instance or creates a new one if it doesn't exist.
- The Client uses the ConcreteFlyweight object and passes the extrinsic state to its methods.

8. Real-world examples
----------------------
- Text editors or word processors that manage character formatting.
- Game engines managing a large number of similar objects, like trees or characters in a game world.

Example code:
-------------

class Flyweight:
    def operation(self, extrinsic_state):
        pass

class ConcreteFlyweight(Flyweight):
    def __init__(self, intrinsic_state):
        self._intrinsic_state = intrinsic_state

    def operation(self, extrinsic_state):
        print(f"Intrinsic state: {self._intrinsic_state}, Extrinsic state: {extrinsic_state}")

class FlyweightFactory:
    def __init__(self):
        self._flyweights = {}

    def get_flyweight(self, key):
        if key not in self._flyweights:
            self._flyweights[key] = ConcreteFlyweight(key)
        return self._flyweights[key]

# Client
def main():
    factory = FlyweightFactory()
    flyweight1 = factory.get_flyweight("shared1")
    flyweight1.operation("unique1")

    flyweight2 = factory.get_flyweight("shared1")
    flyweight2.operation("unique2")

    flyweight3 = factory.get_flyweight("shared2")
    flyweight3.operation("unique3")

if __name__ == "__main__":
    main()

```
