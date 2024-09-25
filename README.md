"""
Week 7 task 2
Question: Examine the code and assess where the software design principles are lacking.
"""
class UnstructuredCode: 
    def xyzzy(self, a, b): 
        result = a + b 
        print(f"Result: {result}") 
class Calculator:
    def add(self, a, b): 
        result = a + b 
        print(f"Addition Result: {result}")

    def multiply(self, a, b): 
        result = a * b 
        print(f"Multiplication Result: {result}") 
def legacy_function(x, y):
    r = x + y
    print(f"Result: {r}")
class InflexibleShape:
    def calculate_area(self): 
        pass 
class Circle(InflexibleShape): 
    def calculate_area(self):
        pass
class Square(InflexibleShape):
    def calculate_area(self):
        pass 
# Main code
if __name__ == "__main__":
    obj = UnstructuredCode() 
    obj.xyzzy(5, 10)
    calc = Calculator()
    calc.add(5, 10) 
    calc.multiply(5, 10) 
    legacy_function(5, 10)
    circle = Circle()
    square = Square()



The provided code exhibits several issues related to software design principles. 
 1. Single Responsibility Principle (SRP)

    - Violation: The `UnstructuredCode` and `Calculator` classes have methods that both perform calculations and handle output (printing results). Ideally,         a class should have a single responsibility—performing calculations should be separate from displaying results.
   - Recommendation: Separate the calculation logic from the presentation logic. Create a `Calculator` class that returns results, and have another class or       function responsible for displaying them.

 2. Open/Closed Principle (OCP)
    - Violation: The `InflexibleShape` class is designed to be a base class for shapes, but it does not provide a concrete implementation or a clear             interface for calculating areas. This suggests it may need to be modified every time a new shape is added.
    - Recommendation: Define an interface with a method for calculating the area. Each shape class (e.g., `Circle`, `Square`) should implement this method,        making it easier to add new shapes without modifying existing code.

 3. Liskov Substitution Principle (LSP)
   - Violation: The `InflexibleShape` class is intended to be a base class, but its `calculate_area` method does nothing. If a client uses an instance of        `InflexibleShape`, it won't behave as expected because the method does not provide functionality.
   - Recommendation: Ensure that derived classes (`Circle`, `Square`) provide concrete implementations of `calculate_area`, so they can be used           interchangeably with their base class.

 4. Interface Segregation Principle (ISP)
     - Violation: The code doesn't have a clear interface, but if it did, the `InflexibleShape` class might be forced to expose methods that aren't relevant        for all derived classes. For instance, if you later want to add shapes that don’t have an area, it could lead to unnecessary implementations.
     - Recommendation: Define specific interfaces for different shapes, ensuring classes only implement methods that are relevant to them.

 5. Dependency Inversion Principle (DIP)
    - Violation: The high-level `Calculator` class directly depends on low-level operations (addition, multiplication) without abstraction. If you wanted to       change the way calculations are done, you would have to modify the `Calculator` class.
    - Recommendation: Introduce abstractions (e.g., an interface for operations) that `Calculator` can depend on, allowing for easier changes to the               underlying logic.

 6. Code Organization and Readability
   - Violation: The code structure lacks organization. There’s a mix of standalone functions and classes without clear separation of concerns or logical      grouping.
  - Recommendation: Organize the code into modules or separate files based on functionality (e.g., calculators, shapes) to improve readability and      maintainability.

