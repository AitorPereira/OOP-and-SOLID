# 🧱 Principios de la Programación Orientada a Objetos (Pilares OOP) – Fundamentos para SOLID  

Los **patrones de diseño** son orientados a objetos, a diferencia de la programación **procedural**, que se centra en ejecutar instrucciones paso a paso.  

En **programación orientada a objetos (POO)** pensamos en las **relaciones e interacciones entre los diferentes componentes (objetos)** en lugar de funciones aisladas.  

Los patrones de diseño nos permiten abstraernos un nivel más, haciendo la programación más **sencilla, organizada y reutilizable**.  

Un **objeto** es un conjunto de variables (**atributos**) y funciones (**métodos**).  

- Ejemplo: Un objeto `Animal` puede tener un atributo `edad` y un método `envejecer()`.  
- Una **clase** es el molde a partir del cual se crean múltiples objetos con sus propios atributos y métodos.  
- La etapa donde se definen los objetos se llama **modelado de datos**. 

---

## 🔑 Los Cuatro Pilares de la POO  

### 1. Encapsulación  
La **encapsulación** asegura que el estado interno de un objeto se mantenga oculto y que solo pueda ser accedido o modificado a través de métodos bien definidos.  

✔️ **Por qué importa:** Previene modificaciones indebidas y garantiza un acceso controlado.  

```python
class CuentaBancaria:
    def __init__(self, titular, saldo):
        self.titular = titular
        self.__saldo = saldo  # atributo privado

    def depositar(self, cantidad):
        if cantidad > 0:
            self.__saldo += cantidad

    def retirar(self, cantidad):
        if 0 < cantidad <= self.__saldo:
            self.__saldo -= cantidad

    def obtener_saldo(self):
        return self.__saldo


cuenta = CuentaBancaria("Aitor", 1000)
cuenta.depositar(500)
print(cuenta.obtener_saldo())  # ✅ 1500
# print(cuenta.__saldo)        # ❌ Error (oculto)
```

2. Abstracción

La abstracción se enfoca en qué hace un objeto en lugar de cómo lo hace.
Interactuamos con los objetos a través de interfaces o clases abstractas sin necesidad de conocer los detalles internos de su implementación.

✔️ Por qué importa: Reduce la complejidad y mejora la reutilización de código.

```python
from abc import ABC, abstractmethod

class Vehiculo(ABC):
    @abstractmethod
    def mover(self):
        pass

class Coche(Vehiculo):
    def mover(self):
        return "Conduciendo en la carretera 🚗"

class Barco(Vehiculo):
    def mover(self):
        return "Navegando en el agua 🚤"

# Solo nos importa que todos los vehículos "se mueven"
vehiculos = [Coche(), Barco()]
for v in vehiculos:
    print(v.mover())
```

3. Herencia

La herencia permite que una clase (hija) reutilice atributos y métodos de otra clase (padre).

✔️ Por qué importa: Fomenta la reutilización de código y establece relaciones jerárquicas.

```python
class Animal:
    def __init__(self, nombre):
        self.nombre = nombre

    def comer(self):
        return f"{self.nombre} está comiendo."

class Perro(Animal):  # Hereda de Animal
    def ladrar(self):
        return f"{self.nombre} dice guau!"

class Gato(Animal):  # Hereda de Animal
    def maullar(self):
        return f"{self.nombre} dice miau!"

perro = Perro("Rex")
gato = Gato("Bigotes")
print(perro.comer())   # Método heredado
print(perro.ladrar())  # Método específico
print(gato.maullar())  # Método específico
```

4. Polimorfismo

El polimorfismo permite que un mismo método tenga distintos comportamientos dependiendo del objeto.

✔️ Por qué importa: Aumenta la flexibilidad y permite que los objetos se usen de forma intercambiable.

```python
class Pajaro:
    def mover(self):
        return "Volando en el cielo 🕊️"

class Pinguino(Pajaro):
    def mover(self):
        return "Nadando en el océano 🐧"

class Avestruz(Pajaro):
    def mover(self):
        return "Corriendo en la tierra 🦤"

pajaros = [Pajaro(), Pinguino(), Avestruz()]
for p in pajaros:
    print(p.mover())  # Mismo método, diferentes comportamientos
```

## 🧩 Por qué Estos Pilares Importan para SOLID

Estos principios de la POO son la base de los principios SOLID.
	•	Encapsulación → Apoya el Principio de Responsabilidad Única (SRP).
	•	Abstracción → Conduce a la Segregación de Interfaces (ISP).
	•	Herencia → Refuerza la Sustitución de Liskov (LSP).
	•	Polimorfismo → Habilita el Principio Abierto/Cerrado (OCP) y mayor flexibilidad.

En conjunto, hacen que el software sea escalable, mantenible y reutilizable.
