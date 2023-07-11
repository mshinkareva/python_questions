Принцип подстановки Барбары Лисков (Liskov Substitution Principle - LSP) гласит, что "функции, которые используют указатели или ссылки на базовый класс, должны иметь возможность использовать объекты производного класса без знания об этом".

❌ Неправильный пример:

Предположим, у нас есть класс Bird и класс Penguin, который является подклассом Bird. Пингвины, хотя и являются птицами, не могут летать, поэтому если мы попытаемся вызвать метод fly() для Penguin, это вызовет проблемы.

```python
class Bird:
    def fly(self):
        return "I can fly!"

class Penguin(Bird):
    def fly(self):
        return "I can't fly."

```
Этот код будет некорректно работать с объектами класса Penguin

✅ Правильный пример:

Идеальное решение было бы разделить классы птиц на тех, кто может летать, и тех, кто нет, на уровне архитектуры:
```python
class Bird:
    pass

class FlyingBird(Bird):
    def fly(self):
        return "I can fly!"

class FlightlessBird(Bird):
    pass

class Penguin(FlightlessBird):
    pass

```
