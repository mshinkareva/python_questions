
Принцип открытости/закрытости (Open/Closed Principle - OCP) утверждает, что
"программные сущности (классы, модули, функции и т.д.) должны быть открыты для расширения, но закрыты для изменения".

❌ Неправильный пример:
```python
class Rectangle:
    def __init__(self, width, height):
        self.width = width
        self.height = height

class AreaCalculator:
    def calculate_area(self, rectangle):
        return rectangle.width * rectangle.height

```
Предположим, теперь вам нужно добавить возможность вычисления площади круга. Вам придется изменить класс AreaCalculator:
```python
class Circle:
    def __init__(self, radius):
        self.radius = radius

class AreaCalculator:
    def calculate_area(self, shape):
        if isinstance(shape, Rectangle):
            return shape.width * shape.height
        elif isinstance(shape, Circle):
            return 3.14 * shape.radius * shape.radius
```
Это изменение класса AreaCalculator нарушает принцип OCP, так как мы изменяем существующий класс для добавления новой функциональности.

✅ Правильный пример:

Вместо этого мы можем определить общий интерфейс (или в контексте Python - абстрактный базовый класс), который каждый объект формы может реализовать:

```python
from abc import ABC, abstractmethod

class Shape(ABC):
    @abstractmethod
    def area(self):
        pass

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

class AreaCalculator:
    def calculate_area(self, shape: Shape):
        return shape.area()

```
