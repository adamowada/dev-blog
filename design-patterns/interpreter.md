Interpreter Design Pattern

1. Pattern Name:
Interpreter

2. Problem:
The Interpreter pattern addresses the challenge of implementing a domain-specific language (DSL) or a grammar. It provides a way to define and evaluate language rules or expressions, allowing you to create custom interpreters for different scenarios.

3. Solution:
The Interpreter pattern uses a class hierarchy to represent the grammar rules. It defines an abstract syntax tree (AST) that represents the structure of the expressions in the language. Each node in the AST corresponds to a language construct, and the tree's structure defines the relationships between these constructs.

4. Consequences:
Benefits:
- Separation of grammar rules and their interpretation, which promotes maintainability and flexibility.
- Easy to extend or modify the grammar rules.

Drawbacks:
- Can become inefficient for large or complex grammars.
- The class hierarchy can become large and unwieldy for extensive languages.

5. Implementation:
In Python, the Interpreter pattern can be implemented using classes to represent the language constructs and inheritance to define the relationships between these constructs. You can use polymorphism to evaluate the expressions based on the type of node in the AST.

6. Participants:
- AbstractExpression: An abstract class/interface that defines the common interface for all expressions in the language.
- TerminalExpression: A class that represents terminal expressions in the language (i.e., expressions that don't have any sub-expressions).
- NonTerminalExpression: A class that represents non-terminal expressions in the language (i.e., expressions that have one or more sub-expressions).
- Context: A class that holds the global state or context needed during the interpretation process.

7. Collaborations:
The interpreter works by recursively traversing the AST and evaluating each expression based on its type (terminal or non-terminal). The evaluation process uses the context to store and access relevant information during interpretation.

8. Real-world examples:
- Implementing simple mathematical expressions evaluator.
- Parsing and evaluating custom configuration files or simple scripting languages.

Example Code:

```python
from abc import ABC, abstractmethod

class AbstractExpression(ABC):
    @abstractmethod
    def interpret(self, context):
        pass

class TerminalExpression(AbstractExpression):
    def __init__(self, value):
        self.value = value

    def interpret(self, context):
        return self.value

class AddExpression(AbstractExpression):
    def __init__(self, left_expression, right_expression):
        self.left_expression = left_expression
        self.right_expression = right_expression

    def interpret(self, context):
        return self.left_expression.interpret(context) + self.right_expression.interpret(context)

class SubtractExpression(AbstractExpression):
    def __init__(self, left_expression, right_expression):
        self.left_expression = left_expression
        self.right_expression = right_expression

    def interpret(self, context):
        return self.left_expression.interpret(context) - self.right_expression.interpret(context)

# Usage example:
def main():
    context = None
    left = TerminalExpression(10)
    right = TerminalExpression(5)

    add_expression = AddExpression(left, right)
    print("Result of addition:", add_expression.interpret(context))

    subtract_expression = SubtractExpression(left, right)
    print("Result of subtraction:", subtract_expression.interpret(context))

if __name__ == "__main__":
    main()

```

This example demonstrates a simple interpreter for mathematical expressions, including addition and subtraction operations. The pattern can be extended for more complex expressions and additional operations as needed.
