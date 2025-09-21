# 🧱 Object-Oriented Programming Principles (OOP Pillars)  
# Foundations for SOLID  

Design patterns are object-oriented by nature, unlike procedural programming, which focuses on executing instructions step by step.  

In object-oriented programming (OOP), we think in terms of the **relationships and interactions between different components (objects)** rather than working with isolated functions.  

Design patterns allow us to take abstraction one step further, making code **simpler, more organized, and reusable**.  

An **object** is a collection of variables (**attributes**) and functions (**methods**).  

- Example: An `Animal` object might have an attribute `age` and a method `grow_older()`.  
- A **class** is the blueprint from which multiple objects are created, each with their own attributes and methods.  
- The stage where we define these objects is called **data modeling**.  

---

## 🔑 The Four OOP Pillars  

### 1. Encapsulation  
Encapsulation ensures that the internal state of an object is hidden and can only be accessed or modified through well-defined methods.  

✔️ **Why it matters:** Prevents unauthorized or accidental modifications and enforces controlled access.  

  ```python
  class BankAccount:
      def __init__(self, owner, balance):
          self.owner = owner
          self.__balance = balance  # private attribute
  
      def deposit(self, amount):
          if amount > 0:
              self.__balance += amount
  
      def withdraw(self, amount):
          if 0 < amount <= self.__balance:
              self.__balance -= amount
  
      def get_balance(self):
          return self.__balance


account = BankAccount("Alice", 1000)
account.deposit(500)
print(account.get_balance())  # ✅ 1500
# print(account.__balance)    # ❌ AttributeError (hidden)

2. Abstraction

Abstraction focuses on what an object does rather than how it does it.  
We interact with objects through interfaces or abstract classes without needing to know their internal implementation.

✔️ Why it matters: Reduces complexity and improves code reusability.

from abc import ABC, abstractmethod

```python
class Vehicle(ABC):
    @abstractmethod
    def move(self):
        pass

class Car(Vehicle):
    def move(self):
        return "Driving on the road 🚗"

class Boat(Vehicle):
    def move(self):
        return "Sailing on the water 🚤"

# We only care that all vehicles "move"
vehicles = [Car(), Boat()]
for v in vehicles:
    print(v.move())

3. Inheritance

Inheritance allows a class (child) to reuse attributes and methods from another class (parent).

✔️ Why it matters: Promotes code reusability and establishes hierarchical relationships.

```python
class Animal:
    def __init__(self, name):
        self.name = name

    def eat(self):
        return f"{self.name} is eating."

class Dog(Animal):  # Inherits from Animal
    def bark(self):
        return f"{self.name} says woof!"

class Cat(Animal):  # Inherits from Animal
    def meow(self):
        return f"{self.name} says meow!"

dog = Dog("Rex")
cat = Cat("Whiskers")
print(dog.eat())   # Inherited method
print(dog.bark())  # Specific method
print(cat.meow())  # Specific method

4. Polymorphism

Polymorphism allows the same method name to behave differently depending on the object.

✔️ Why it matters: Increases flexibility by letting objects be used interchangeably while still behaving correctly.

```python
class Bird:
    def move(self):
        return "Flying in the sky 🕊️"

class Penguin(Bird):
    def move(self):
        return "Swimming in the ocean 🐧"

class Ostrich(Bird):
    def move(self):
        return "Running on the ground 🦤"

birds = [Bird(), Penguin(), Ostrich()]
for b in birds:
    print(b.move())  # Same method, different behavior

## 🧩 Why These Pillars Matter for SOLID

These OOP principles are the foundation of the SOLID principles.
	•	Encapsulation → Supports Single Responsibility Principle (SRP).
	•	Abstraction → Leads to Interface Segregation (ISP).
	•	Inheritance → Encourages Liskov Substitution (LSP).
	•	Polymorphism → Enables Open/Closed Principle (OCP) and flexibility.

Together, they make software scalable, maintainable, and reusable.
