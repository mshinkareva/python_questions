Принцип инверсии зависимостей (Dependency Inversion Principle - DIP) гласит, что "модули верхних уровней не должны зависеть от модулей нижних уровней, и они оба должны зависеть от абстракций". Кроме того, абстракции не должны зависеть от деталей, детали должны зависеть от абстракций.


❌ Неправильный пример:

```python
class Dog:
    def __init__(self, name):
        self.name = name

    def feed(self):
        return f"Feeding dog {self.name}"

class Lion:
    def __init__(self, name):
        self.name = name

    def feed(self):
        return f"Feeding lion {self.name}"

class Zookeeper:
    def __init__(self, dog: Dog, lion: Lion):
        self.dog = dog
        self.lion = lion

    def feed_dog(self):
        return self.dog.feed()

    def feed_lion(self):
        return self.lion.feed()
```

В этом случае класс Zookeeper зависит от конкретных классов Dog и Lion, что нарушает принцип инверсии зависимостей. Если мы захотим добавить новое животное в зоопарк, нам придется менять код класса Zookeeper, что нарушает принцип открытости/закрытости.


✅ Правильный пример:

```python
from abc import ABC, abstractmethod

class Animal(ABC):
    def __init__(self, name):
        self.name = name

    @abstractmethod
    def feed(self):
        pass

class Dog(Animal):
    def feed(self):
        return f"Feeding dog {self.name}"

class Lion(Animal):
    def feed(self):
        return f"Feeding lion {self.name}"

class Zookeeper:
    def __init__(self, animals: list):
        self.animals = animals

    def feed_animals(self):
        for animal in self.animals:
            print(animal.feed())
```