# Лекция 13: Основы ООП

## Введение

Объектно-ориентированное программирование (ООП) - это парадигма программирования, основанная на понятии "объектов", которые могут содержать данные (атрибуты) и код (методы). ООП позволяет структурировать программы таким образом, чтобы разные типы данных и функции, которые с ними работают, были объединены в отдельные, легко используемые единицы - классы. В этой лекции мы рассмотрим основные концепции ООП в Python: классы, объекты, атрибуты, методы и основные принципы ООП.

## Основное содержание

### Что такое класс и объект

**Класс** - это шаблон или чертеж для создания объектов. Он определяет атрибуты и методы, которые будут у объектов этого класса.

**Объект (экземпляр класса)** - это конкретная реализация класса с конкретными значениями атрибутов.

```python
# Пример простого класса
class Car:
    """Класс для представления автомобиля"""
    
    # Атрибут класса (один на все экземпляры)
    wheels = 4
    
    def __init__(self, brand, model, year):
        """Конструктор класса - инициализирует атрибуты экземпляра"""
        self.brand = brand    # Атрибут экземпляра
        self.model = model    # Атрибут экземпляра
        self.year = year      # Атрибут экземпляра
        self.mileage = 0      # Атрибут экземпляра с значением по умолчанию
    
    def start_engine(self):
        """Метод класса"""
        return f"{self.brand} {self.model} двигатель запущен!"
    
    def drive(self, distance):
        """Метод класса для увеличения пробега"""
        self.mileage += distance
        return f"Проехали {distance} км. Общий пробег: {self.mileage} км."

# Создание объектов (экземпляров класса)
car1 = Car("Toyota", "Camry", 2020)
car2 = Car("Honda", "Civic", 2019)

# Использование объектов
print(car1.start_engine())  # Toyota Camry двигатель запущен!
print(car2.drive(100))      # Проехали 100 км. Общий пробег: 100 км.
print(f"У {Car.wheels} колеса")  # У 4 колеса
```

### Конструктор `__init__`

Метод `__init__` - это специальный метод, который вызывается при создании нового объекта. Он инициализирует атрибуты экземпляра:

```python
class Student:
    def __init__(self, name, age, major):
        self.name = name
        self.age = age
        self.major = major
        self.grades = []  # Пустой список оценок
    
    def add_grade(self, grade):
        """Добавляет оценку"""
        self.grades.append(grade)
    
    def get_average_grade(self):
        """Возвращает среднюю оценку"""
        if not self.grades:
            return 0
        return sum(self.grades) / len(self.grades)

# Создание экземпляра
student = Student("Иван Иванов", 20, "Информатика")
student.add_grade(5)
student.add_grade(4)
student.add_grade(5)
print(f"Средний балл: {student.get_average_grade()}")  # Средний балл: 4.66666666667
```

### Атрибуты класса и экземпляра

```python
class BankAccount:
    # Атрибут класса (один на все экземпляры)
    bank_name = "Наш банк"
    total_accounts = 0  # Счетчик всех созданных аккаунтов
    
    def __init__(self, owner, balance=0):
        # Атрибуты экземпляра
        self.owner = owner
        self.balance = balance
        self.account_number = BankAccount.total_accounts + 1
        
        # Увеличиваем счетчик при создании нового аккаунта
        BankAccount.total_accounts += 1
    
    def deposit(self, amount):
        """Внести деньги"""
        self.balance += amount
        return f"Внесено {amount}. Баланс: {self.balance}"
    
    def withdraw(self, amount):
        """Снять деньги"""
        if amount <= self.balance:
            self.balance -= amount
            return f"Снято {amount}. Баланс: {self.balance}"
        else:
            return "Недостаточно средств"

# Пример использования
account1 = BankAccount("Иван", 1000)
account2 = BankAccount("Мария", 2000)

print(f"Банк: {BankAccount.bank_name}")  # Банк: Наш банк
print(f"Всего аккаунтов: {BankAccount.total_accounts}")  # Всего аккаунтов: 2
print(account1.deposit(500))  # Внесено 500. Баланс: 1500
```

### Методы класса и статические методы

```python
class MathUtils:
    PI = 3.14159
    
    def __init__(self):
        self.description = "Утилиты для математических вычислений"
    
    # Обычный метод экземпляра (принимает self)
    def circle_area(self, radius):
        return self.PI * radius ** 2
    
    # Метод класса (принимает cls)
    @classmethod
    def sphere_volume(cls, radius):
        return (4/3) * cls.PI * radius ** 3
    
    # Статический метод (не принимает ни self, ни cls)
    @staticmethod
    def factorial(n):
        if n <= 1:
            return 1
        return n * MathUtils.factorial(n - 1)

# Примеры использования
math_obj = MathUtils()
print(math_obj.circle_area(5))  # 78.53975
print(MathUtils.sphere_volume(3))  # 113.09724
print(MathUtils.factorial(5))  # 120
```

### Инкапсуляция

Инкапсуляция - это принцип, согласно которому внутренние детали объекта скрыты от внешнего мира. В Python используется соглашение об именовании:

```python
class Person:
    def __init__(self, name, age):
        self.name = name
        self._age = age  # Защищенный атрибут (одно подчеркивание)
        self.__id = self.__generate_id()  # Приватный атрибут (два подчеркивания)
    
    def get_age(self):
        """Публичный метод для получения возраста"""
        return self._age
    
    def set_age(self, age):
        """Публичный метод для установки возраста с проверкой"""
        if 0 <= age <= 150:
            self._age = age
        else:
            print("Недопустимый возраст")
    
    def __generate_id(self):
        """Приватный метод для генерации ID"""
        import random
        return random.randint(1000, 999)
    
    def get_id(self):
        """Публичный метод для получения ID"""
        return self.__id

# Пример использования
person = Person("Алексей", 30)
print(person.name)  # Алексей
print(person.get_age())  # 30
person.set_age(31)
print(person.get_id())  # Случайное число

# Обратите внимание: person.__id недоступен напрямую
# Но можно получить косвенно через name mangling: person._Person__id
```

### Наследование

Наследование позволяет создавать новые классы на основе существующих, расширяя их функциональность:

```python
# Базовый (родительский) класс
class Animal:
    def __init__(self, name, species):
        self.name = name
        self.species = species
    
    def make_sound(self):
        return f"{self.name} издает звук"
    
    def info(self):
        return f"{self.name} - {self.species}"

# Дочерний класс (наследуется от Animal)
class Dog(Animal):
    def __init__(self, name, breed):
        super().__init__(name, "Собака")  # Вызов конструктора родительского класса
        self.breed = breed
    
    def make_sound(self):  # Переопределение метода
        return f"{self.name} говорит: Гав!"
    
    def fetch(self):  # Новый метод для дочернего класса
        return f"{self.name} принес палку!"

# Еще один дочерний класс
class Cat(Animal):
    def __init__(self, name, color):
        super().__init__(name, "Кошка")
        self.color = color
    
    def make_sound(self):
        return f"{self.name} говорит: Мяу!"
    
    def climb(self):
        return f"{self.name} залез на дерево!"

# Примеры использования
dog = Dog("Бобик", "Лабрадор")
cat = Cat("Мурка", "Рыжая")

print(dog.info())  # Бобик - Собака
print(dog.make_sound())  # Бобик говорит: Гав!
print(dog.fetch())  # Бобик принес палку!

print(cat.info())  # Мурка - Кошка
print(cat.make_sound())  # Мурка говорит: Мяу!
print(cat.climb())  # Мурка залез на дерево!
```

### Полиморфизм

Полиморфизм позволяет использовать объекты разных классов с одинаковым интерфейсом:

```python
class Shape:
    def area(self):
        pass  # Абстрактный метод
    
    def perimeter(self):
        pass  # Абстрактный метод

class Rectangle(Shape):
    def __init__(self, width, height):
        self.width = width
        self.height = height
    
    def area(self):
        return self.width * self.height
    
    def perimeter(self):
        return 2 * (self.width + self.height)

class Circle(Shape):
    def __init__(self, radius):
        self.radius = radius
    
    def area(self):
        return 3.14159 * self.radius ** 2
    
    def perimeter(self):
        return 2 * 3.14159 * self.radius

# Функция, использующая полиморфизм
def print_shape_info(shape):
    print(f"Площадь: {shape.area():.2f}")
    print(f"Периметр: {shape.perimeter():.2f}")

# Примеры использования
shapes = [Rectangle(5, 3), Circle(4), Rectangle(2, 8)]

for shape in shapes:
    print_shape_info(shape)
    print("---")
```

### Магические методы (dunder methods)

Магические методы позволяют определять поведение объектов при использовании встроенных операций:

```python
class Vector:
    def __init__(self, x, y):
        self.x = x
        self.y = y
    
    def __repr__(self):
        return f"Vector({self.x}, {self.y})"
    
    def __str__(self):
        return f"({self.x}, {self.y})"
    
    def __add__(self, other):
        """Определяет поведение оператора +"""
        return Vector(self.x + other.x, self.y + other.y)
    
    def __mul__(self, scalar):
        """Определяет поведение оператора * (вектор на число)"""
        return Vector(self.x * scalar, self.y * scalar)
    
    def __eq__(self, other):
        """Определяет поведение оператора =="""
        return self.x == other.x and self.y == other.y
    
    def __len__(self):
        """Определяет поведение функции len()"""
        return int((self.x**2 + self.y**2)**0.5)
    
    def __getitem__(self, index):
        """Определяет поведение при индексации"""
        if index == 0:
            return self.x
        elif index == 1:
            return self.y
        else:
            raise IndexError("Vector index out of range")

# Примеры использования
v1 = Vector(2, 3)
v2 = Vector(4, 5)

print(v1)  # (2, 3)
print(repr(v2))  # Vector(4, 5)
print(v1 + v2)  # (6, 8)
print(v1 * 3)  # (6, 9)
print(len(v1))  # 3 (округленная длина вектора)
print(v1[0])  # 2
print(v1 == Vector(2, 3))  # True
```

### Пример комплексного класса

```python
class LibraryBook:
    """Класс для представления книги в библиотеке"""
    
    # Атрибут класса
    total_books = 0
    
    def __init__(self, title, author, isbn, copies=1):
        # Атрибуты экземпляра
        self.title = title
        self.author = author
        self.isbn = isbn
        self.total_copies = copies
        self.available_copies = copies
        self.borrowed_by = []  # Список заимствовавших
        
        # Увеличиваем счетчик книг
        LibraryBook.total_books += 1
    
    def borrow(self, borrower_name):
        """Заимствовать книгу"""
        if self.available_copies > 0:
            self.available_copies -= 1
            self.borrowed_by.append(borrower_name)
            return f"Книга '{self.title}' выдана {borrower_name}"
        else:
            return f"Книга '{self.title}' недоступна для выдачи"
    
    def return_book(self, borrower_name):
        """Вернуть книгу"""
        if borrower_name in self.borrowed_by:
            self.available_copies += 1
            self.borrowed_by.remove(borrower_name)
            return f"Книга '{self.title}' возвращена {borrower_name}"
        else:
            return f"{borrower_name} не брал(а) эту книгу"
    
    def get_info(self):
        """Получить информацию о книге"""
        return {
            "title": self.title,
            "author": self.author,
            "isbn": self.isbn,
            "available": self.available_copies,
            "total": self.total_copies,
            "borrowers": self.borrowed_by.copy()
        }
    
    def __str__(self):
        return f"'{self.title}' by {self.author} ({self.available_copies}/{self.total_copies} доступно)"
    
    @classmethod
    def get_total_books(cls):
        """Возвращает общее количество книг"""
        return cls.total_books

# Пример использования
book1 = LibraryBook("1984", "Джордж Оруэлл", "978-0-452-28423-4", 3)
book2 = LibraryBook("Гордость и предубеждение", "Джейн Остин", "978-0-14-143951-8", 2)

print(book1)  # '1984' by Джордж Оруэлл (3/3 доступно)
print(book1.borrow("Иванов"))  # Книга '1984' выдана Иванов
print(book1)  # '1984' by Джордж Оруэлл (2/3 доступно)
print(book1.return_book("Иванов"))  # Книга '1984' возвращена Иванов
print(f"Всего книг в библиотеке: {LibraryBook.get_total_books()}")  # Всего книг в библиотеке: 2
```

## Практические примеры

### Пример 1: Система учета студентов

```python
class Student:
    def __init__(self, student_id, name, major):
        self.student_id = student_id
        self.name = name
        self.major = major
        self.courses = []
        self.grades = {}
    
    def enroll_course(self, course):
        if course not in self.courses:
            self.courses.append(course)
            self.grades[course] = []
    
    def add_grade(self, course, grade):
        if course in self.grades:
            self.grades[course].append(grade)
        else:
            print(f"Студент не записан на курс {course}")
    
    def get_gpa(self):
        total_points = 0
        total_courses = 0
        
        for course_grades in self.grades.values():
            if course_grades:  # Если есть оценки по курсу
                total_points += sum(course_grades) / len(course_grades)
                total_courses += 1
        
        return total_points / total_courses if total_courses > 0 else 0
    
    def get_transcript(self):
        transcript = f"Студенческая карта: {self.name} (ID: {self.student_id})\n"
        transcript += f"Специальность: {self.major}\n"
        transcript += f"Средний балл: {self.get_gpa():.2f}\n"
        transcript += "Курсы и оценки:\n"
        
        for course, grades in self.grades.items():
            avg_grade = sum(grades) / len(grades) if grades else 0
            transcript += f"  {course}: {grades} (среднее: {avg_grade:.2f})\n"
        
        return transcript

# Пример использования
student = Student(12345, "Иван Петров", "Информатика")
student.enroll_course("Программирование на Python")
student.enroll_course("Алгоритмы и структуры данных")

student.add_grade("Программирование на Python", 5)
student.add_grade("Программирование на Python", 4)
student.add_grade("Алгоритмы и структуры данных", 5)

print(student.get_transcript())
```

### Пример 2: Банковская система

```python
from datetime import datetime

class Transaction:
    def __init__(self, transaction_type, amount):
        self.type = transaction_type
        self.amount = amount
        self.timestamp = datetime.now()
    
    def __str__(self):
        return f"{self.timestamp.strftime('%Y-%m-%d %H:%M:%S')} - {self.type}: {self.amount}"

class BankAccount:
    def __init__(self, account_holder, initial_balance=0):
        self.account_holder = account_holder
        self.balance = initial_balance
        self.transaction_history = []
        
        # Регистрируем начальный депозит, если баланс > 0
        if initial_balance > 0:
            self.transaction_history.append(Transaction("Начальный депозит", initial_balance))
    
    def deposit(self, amount):
        if amount > 0:
            self.balance += amount
            self.transaction_history.append(Transaction("Депозит", amount))
            return True
        return False
    
    def withdraw(self, amount):
        if 0 < amount <= self.balance:
            self.balance -= amount
            self.transaction_history.append(Transaction("Снятие", -amount))
            return True
        return False
    
    def get_balance(self):
        return self.balance
    
    def get_transaction_history(self, limit=None):
        history = self.transaction_history[-limit:] if limit else self.transaction_history
        return [str(transaction) for transaction in history]

# Пример использования
account = BankAccount("Алексей Иванов", 1000)
account.deposit(500)
account.withdraw(200)
account.deposit(300)

print(f"Баланс: {account.get_balance()}")  # Баланс: 1600
print("История транзакций:")
for transaction in account.get_transaction_history():
    print(transaction)
```

## Заключение

В этой лекции мы подробно рассмотрели основы объектно-ориентированного программирования в Python:

1. **Классы и объекты** - как создавать использовать
2. **Атрибуты и методы** - различия между атрибутами класса и экземпляра
3. **Конструктор `__init__`** - инициализация объектов
4. **Инкапсуляция** - управление доступом к данным
5. **Наследование** - создание дочерних классов
6. **Полиморфизм** - использование объектов разных классов с общим интерфейсом
7. **Магические методы** - определение поведения при стандартных операциях
8. **Практические примеры** - применение ООП в реальных задачах

ООП позволяет создавать более структурированный, читаемый и поддерживаемый код, особенно в крупных проектах. В следующей лекции мы рассмотрим повторение и обобщение алгоритмических конструкций.
