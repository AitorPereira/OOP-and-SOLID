# Principios SOLID en Python  

Un desarrollador junior suele enfocarse únicamente en hacer que el código *funcione*.  
Un desarrollador senior, en cambio, se preocupa por que el código sea *mantenible*, *extensible* y *fácil de mejorar* con el tiempo.  

El término **SOLID** fue introducido por *Michael Feathers* como un acrónimo de cinco principios de diseño promovidos originalmente por *Robert C. Martin* (Uncle Bob).  

---

## Propósito de SOLID
Los principios SOLID tienen como objetivo:  
* Hacer el código más **mantenible**.  
* Simplificar la **corrección de errores y futuros cambios**.  
* Permitir la **incorporación de nuevas funcionalidades** sin romper el código existente.  

---

## Significado de SOLID
* **S**: Single Responsibility Principle (Principio de Responsabilidad Única)  
* **O**: Open/Closed Principle (Principio Abierto/Cerrado)  
* **L**: Liskov Substitution Principle (Principio de Sustitución de Liskov)  
* **I**: Interface Segregation Principle (Principio de Segregación de Interfaces)  
* **D**: Dependency Inversion Principle (Principio de Inversión de Dependencia)  

---

## Los 5 Principios de SOLID con Ejemplos en Python  

---

### 1. Single Responsibility Principle (SRP)  

Una clase debe tener **solo una responsabilidad**.  
Si se necesitan nuevas responsabilidades, se deben crear nuevas clases en lugar de sobrecargar las existentes.  

**❌ Mal ejemplo: una clase maneja tanto los datos como la generación de reportes**
```python
class Report:
    def __init__(self, data):
        self.data = data

    def calculate_total(self):
        return sum(self.data)

    def print_report(self):  # Responsabilidad extra
        print("Report:", self.calculate_total())
```
**✅ Buen ejemplo: responsabilidades separadas**
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

Las entidades de software deben estar abiertas a la extensión pero cerradas a la modificación.
Se logra mediante herencia y polimorfismo.
```python
from abc import ABC, abstractmethod
```
**✅ Clase base (cerrada a la modificación)**
```python
class Shape(ABC):
    @abstractmethod
    def area(self):
        pass
```
**✅ Nuevas figuras extienden la funcionalidad sin cambiar el código existente**
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
    print(s.area())  # Funciona para todas las figuras sin modificar código antiguo
```

### 3. Liskov Substitution Principle (LSP)

Las subclases deben poder sustituir a sus clases padre sin alterar el comportamiento del sistema.

**❌ Mal ejemplo: el Pingüino no puede volar, pero Bird espera que sí pueda**
```python
class Bird:
    def fly(self):
        print("Flying...")

class Penguin(Bird):
    def fly(self):
        raise Exception("Penguins cannot fly!")  # Viola LSP
```
**✅ Buen ejemplo: reorganizar la jerarquía**
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
    b.move()  # Ambos funcionan correctamente sin romper expectativas
```

### 4. Interface Segregation Principle (ISP)

Es mejor tener muchas interfaces pequeñas y específicas que una interfaz grande y general.
```python
from abc import ABC, abstractmethod
```

**✅ Interfaces pequeñas y enfocadas**
```python
class Printer(ABC):
    @abstractmethod
    def print(self, document): pass

class Scanner(ABC):
    @abstractmethod
    def scan(self): pass
```

**✅ Las clases solo implementan lo que necesitan**
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

Los módulos de alto nivel no deben depender de módulos de bajo nivel.
Ambos deben depender de abstracciones.
```python
from abc import ABC, abstractmethod
```
**✅ Abstracción**+
```python
class Database(ABC):
    @abstractmethod
    def save(self, data): pass
```
**✅ Implementaciones de bajo nivel**
```python
class MongoDB(Database):
    def save(self, data):
        print("Saving to MongoDB:", data)

class SQLDatabase(Database):
    def save(self, data):
        print("Saving to SQL Database:", data)
```
**✅ El módulo de alto nivel depende de la abstracción, no de clases concretas**
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

✅ Con estos principios en mente, tu código se vuelve modular, escalable y robusto: cualidades que diferencian el software de nivel profesional de los simples scripts rápidos.
