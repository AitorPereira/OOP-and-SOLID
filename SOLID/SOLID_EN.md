# SOLID Principles in Python  

A junior developer often focuses only on making code *work*.  
A senior developer, on the other hand, cares about making code *maintainable*, *extensible*, and *easy to improve* over time.  

The term **SOLID** was introduced by *Michael Feathers* as an acronym for five design principles originally promoted by *Robert C. Martin* (Uncle Bob).  

---

## Purpose of SOLID
The SOLID principles aim to:  
* Make code more **maintainable**.  
* Simplify **bug fixing and future changes**.  
* Allow **new features** to be added without breaking existing code.  

---

## Meaning of SOLID
* **S**: Single Responsibility Principle  
* **O**: Open/Closed Principle  
* **L**: Liskov Substitution Principle  
* **I**: Interface Segregation Principle  
* **D**: Dependency Inversion Principle  

---

## The 5 SOLID Principles with Python Examples  

---

### 1. Single Responsibility Principle (SRP)  

A class should have **only one responsibility**.  
If new responsibilities are needed, create new classes instead of overloading existing ones.  


**❌ Bad example: one class handles both data and report generation**
```python
class Report:
    def __init__(self, data):
        self.data = data

    def calculate_total(self):
        return sum(self.data)

    def print_report(self):  # Extra responsibility
        print("Report:", self.calculate_total())
```

**✅ Good example: separate responsibilities**
```python
class Report:
    def __init__(self, data):
        self.data = data

    def calculate_total(self):
        return sum(self.data)

class ReportPrinter:
    def print_report(self, report: Report):
        print("Report:", report.calculate_total())

report = Report([10, 20, 30])
printer = ReportPrinter()
printer.print_report(report)
```

### 2. Open/Closed Principle (OCP)

Software entities should be open for extension but closed for modification.
Achieved through inheritance and polymorphism.

```python
from abc import ABC, abstractmethod
```

**✅ Base class (closed for modification)**
```python
class Shape(ABC):
    @abstractmethod
    def area(self):
        pass
```

**✅ New shapes extend functionality without changing existing code**
```python
class Rectangle(Shape):
    def __init__(self, width, height):
        self.width = width
        self.height = height

    def area(self):
        return self.width * self.height

class Circle(Shape):
    def __init__(self, radius):
        self.radius = radius

    def area(self):
        return 3.14 * self.radius * self.radius

shapes = [Rectangle(3, 4), Circle(5)]
for s in shapes:
    print(s.area())  # Works for all shapes without modifying old code
```

###3. Liskov Substitution Principle (LSP)

Subclasses must be substitutable for their parent classes without altering system behavior.

**❌ Bad example: Penguin cannot fly, but Bird expects fly()**
```python
class Bird:
    def fly(self):
        print("Flying...")

class Penguin(Bird):
    def fly(self):
        raise Exception("Penguins cannot fly!")  # Violates LSP
```
**✅ Good example: Reorganize hierarchy**
```python
from abc import ABC, abstractmethod

class Bird(ABC):
    @abstractmethod
    def move(self):
        pass

class Sparrow(Bird):
    def move(self):
        print("Flying...")

class Penguin(Bird):
    def move(self):
        print("Swimming...")

birds = [Sparrow(), Penguin()]
for b in birds:
    b.move()  # Both work correctly without breaking expectations
```

### 4. Interface Segregation Principle (ISP)

It’s better to have many small, specific interfaces than one large, general interface.
```python
from abc import ABC, abstractmethod
```
**✅ Small, focused interfaces**
```python
class Printer(ABC):
    @abstractmethod
    def print(self, document): pass

class Scanner(ABC):
    @abstractmethod
    def scan(self): pass
```

**✅ Classes only implement what they need**
```python
class SimplePrinter(Printer):
    def print(self, document):
        print("Printing:", document)

class MultiFunctionMachine(Printer, Scanner):
    def print(self, document):
        print("Printing:", document)

    def scan(self):
        print("Scanning document...")

printer = SimplePrinter()
printer.print("Hello World")

mfp = MultiFunctionMachine()
mfp.print("Hello")
mfp.scan()
```

### 5. Dependency Inversion Principle (DIP)

High-level modules should not depend on low-level modules.
Both should depend on abstractions.

```python
from abc import ABC, abstractmethod
```
**✅ Abstraction**
```python
class Database(ABC):
    @abstractmethod
    def save(self, data): pass
```
**✅ Low-level implementations**
```python
class MongoDB(Database):
    def save(self, data):
        print("Saving to MongoDB:", data)

class SQLDatabase(Database):
    def save(self, data):
        print("Saving to SQL Database:", data)
```
**✅ High-level module depends on abstraction, not concrete classes**
```python
class Application:
    def __init__(self, db: Database):
        self.db = db

    def store(self, data):
        self.db.save(data)

app1 = Application(MongoDB())
app1.store("User data")

app2 = Application(SQLDatabase())
app2.store("Order data")
```

✅ With these principles in mind, your code becomes modular, scalable, and robust-qualities that separate production-grade software from quick scripts.
