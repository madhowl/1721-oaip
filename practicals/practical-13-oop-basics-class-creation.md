# Практическая работа 13: Основы ООП: создание класса

## Цель работы

Научиться создавать классы в Python, освоить основные концепции объектно-ориентированного программирования: классы, объекты, атрибуты, методы, конструкторы, а также понять принципы инкапсуляции, наследования и полиморфизма.

## Теоретическая часть

Объектно-ориентированное программирование (ООП) - это парадигма программирования, основанная на понятии "объектов", которые могут содержать данные (атрибуты) и код (методы). Класс - это шаблон для создания объектов, определяющий атрибуты и методы, которые будут у объектов этого класса.

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
```

### Основные концепции ООП:

1. **Инкапсуляция** - сокрытие внутренней реализации объекта и предоставление контролируемого доступа к его свойствам и методам
2. **Наследование** - возможность создания новых классов на основе существующих
3. **Полиморфизм** - способность объектов разных классов использовать одинаковый интерфейс

## Практические задания

### Задание 1: Создание простого класса

Создайте класс `Student`, который будет представлять студента. Класс должен содержать атрибуты: имя, возраст, специальность и методы: представиться, увеличить возраст на 1.

**Пример выполнения:**
```
Имя: Иван Иванов
Возраст: 20
Специальность: Информатика
Привет, я Иван Иванов, мне 20 лет, я обучаюсь по специальности Информатика
```

**Код для выполнения:**
```python
class Student:
    """Класс для представления студента"""
    
    def __init__(self, name, age, major):
        """Инициализация атрибутов студента"""
        self.name = name
        self.age = age
        self.major = major
    
    def introduce(self):
        """Метод для представления студента"""
        return f"Привет, я {self.name}, мне {self.age} лет, я обучаюсь по специальности {self.major}"
    
    def birthday(self):
        """Увеличивает возраст на 1"""
        self.age += 1
        return f"С днем рождения! Теперь вам {self.age} лет"

# Создание экземпляра класса
student1 = Student("Иван Иванов", 20, "Информатика")

# Вывод информации о студенте
print(f"Имя: {student1.name}")
print(f"Возраст: {student1.age}")
print(f"Специальность: {student1.major}")
print(student1.introduce())
```

---

### Задание 2: Класс с вычисляемыми атрибутами

Создайте класс `Rectangle` (прямоугольник), который будет иметь атрибуты длины и ширины, а также методы для вычисления площади и периметра.

**Пример выполнения:**
```
Введите длину: 5
Введите ширину: 3
Площадь: 15
Периметр: 16
```

**Код для выполнения:**
```python
class Rectangle:
    """Класс для представления прямоугольника"""
    
    def __init__(self, length, width):
        """Инициализация атрибутов прямоугольника"""
        self.length = length
        self.width = width
    
    def area(self):
        """Вычисляет площадь прямоугольника"""
        return self.length * self.width
    
    def perimeter(self):
        """Вычисляет периметр прямоугольника"""
        return 2 * (self.length + self.width)
    
    def is_square(self):
        """Проверяет, является ли прямоугольник квадратом"""
        return self.length == self.width

# Создание прямоугольника
length = float(input("Введите длину: "))
width = float(input("Введите ширину: "))

rect = Rectangle(length, width)

print(f"Площадь: {rect.area()}")
print(f"Периметр: {rect.perimeter()}")
print(f"Является квадратом: {rect.is_square()}")
```

---

### Задание 3: Класс с атрибутами класса

Создайте класс `BankAccount` (банковский счет), который будет использовать как атрибуты экземпляра, так и атрибуты класса.

**Код для выполнения:**
```python
class BankAccount:
    """Класс для банковского счета"""
    
    # Атрибут класса - общее количество счетов
    total_accounts = 0
    
    def __init__(self, owner, initial_balance=0):
        """Инициализация атрибутов счета"""
        self.owner = owner
        self.balance = initial_balance
        self.account_number = f"BA{BankAccount.total_accounts + 1:06d}"
        
        # Увеличиваем общее количество счетов
        BankAccount.total_accounts += 1
    
    def deposit(self, amount):
        """Внести деньги на счет"""
        if amount > 0:
            self.balance += amount
            return f"Внесено {amount}. Баланс: {self.balance}"
        return "Сумма должна быть положительной"
    
    def withdraw(self, amount):
        """Снять деньги со счета"""
        if 0 < amount <= self.balance:
            self.balance -= amount
            return f"Снято {amount}. Баланс: {self.balance}"
        elif amount > self.balance:
            return "Недостаточно средств"
        else:
            return "Сумма должна быть положительной"
    
    def get_info(self):
        """Возвращает информацию о счете"""
        return f"Владелец: {self.owner}, Баланс: {self.balance}, Номер: {self.account_number}"

# Создание счетов
account1 = BankAccount("Иванов И.И.", 1000)
account2 = BankAccount("Петров П.П.", 500)

print(account1.get_info())
print(account1.deposit(200))
print(account1.withdraw(150))

print(account2.get_info())
print(f"Всего счетов создано: {BankAccount.total_accounts}")
```

---

### Задание 4: Класс с защищенными и приватными атрибутами

Создайте класс `Person`, который демонстрирует инкапсуляцию с использованием защищенных и приватных атрибутов.

**Код для выполнения:**
```python
class Person:
    """Класс для представления человека"""
    
    def __init__(self, name, age, ssn):
        self.name = name              # Публичный атрибут
        self._age = age               # Защищенный атрибут
        self.__ssn = ssn              # Приватный атрибут (сокрытие данных)
    
    def get_age(self):
        """Публичный метод для получения возраста"""
        return self._age
    
    def set_age(self, age):
        """Публичный метод для установки возраста с проверкой"""
        if 0 <= age <= 150:
            self._age = age
            return True
        else:
            print("Некорректный возраст")
            return False
    
    def get_ssn(self):
        """Публичный метод для получения SSN (в реальных приложениях не рекомендуется)"""
        return f"***-**-{self.__ssn[-4:]}"  # Показываем только последние 4 цифры
    
    def __str__(self):
        """Магический метод для строкового представления объекта"""
        return f"Человек: {self.name}, Возраст: {self._age}"

# Создание объекта
person = Person("Алексей", 30, "123-45-6789")

print(person)  # Использует метод __str__
print(f"Возраст: {person.get_age()}")
print(f"SSN: {person.get_ssn()}")

# Изменение возраста
person.set_age(31)
print(f"Новый возраст: {person.get_age()}")

# Попытка доступа к приватному атрибуту (не рекомендуется)
# print(person.__ssn)  # Это вызовет AttributeError
# Но можно получить через name mangling:
# print(person._Person__ssn)  # Это сработает, но не рекомендуется использовать
```

---

### Задание 5: Наследование

Создайте базовый класс `Vehicle` и производные классы `Car` и `Motorcycle`, демонстрируя наследование.

**Код для выполнения:**
```python
class Vehicle:
    """Базовый класс для транспортного средства"""
    
    def __init__(self, brand, model, year):
        self.brand = brand
        self.model = model
        self.year = year
        self.is_running = False
    
    def start(self):
        """Запускает транспортное средство"""
        self.is_running = True
        return f"{self.brand} {self.model} запущен"
    
    def stop(self):
        """Останавливает транспортное средство"""
        self.is_running = False
        return f"{self.brand} {self.model} остановлен"
    
    def honk(self):
        """Сигнал"""
        return "Бип-бип!"

class Car(Vehicle):
    """Класс для автомобиля"""
    
    def __init__(self, brand, model, year, doors=4):
        super().__init__(brand, model, year)  # Вызов конструктора родительского класса
        self.doors = doors
    
    def honk(self):
        """Переопределение метода сигнала для автомобиля"""
        return "Биип-биип!"
    
    def get_info(self):
        """Информация о машине"""
        return f"Автомобиль {self.brand} {self.model}, {self.year} года, {self.doors} двери"

class Motorcycle(Vehicle):
    """Класс для мотоцикла"""
    
    def __init__(self, brand, model, year, engine_size):
        super().__init__(brand, model, year)
        self.engine_size = engine_size
    
    def honk(self):
        """Переопределение метода сигнала для мотоцикла"""
        return "Врум-врум!"
    
    def wheelie(self):
        """Мотоцикл может делать вилли"""
        return "Мотоцикл делает вилли!"

# Создание объектов
car = Car("Toyota", "Camry", 2020, 4)
motorcycle = Motorcycle("Harley-Davidson", "Street 750", 2019, 750)

print(car.get_info())
print(car.start())
print(car.honk())
print(car.stop())

print(f"\n{motorcycle.brand} {motorcycle.model}")
print(motorcycle.start())
print(motorcycle.honk())
print(motorcycle.wheelie())
print(motorcycle.stop())
```

---

### Задание 6: Полиморфизм

Продемонстрируйте полиморфизм с помощью метода, который работает с разными классами.

**Код для выполнения:**
```python
class Animal:
    """Базовый класс для животного"""
    
    def __init__(self, name):
        self.name = name
    
    def speak(self):
        """Метод, который будет переопределен в подклассах"""
        pass

class Dog(Animal):
    """Класс собаки"""
    
    def speak(self):
        return f"{self.name} говорит: Гав!"

class Cat(Animal):
    """Класс кошки"""
    
    def speak(self):
        return f"{self.name} говорит: Мяу!"

class Bird(Animal):
    """Класс птицы"""
    
    def speak(self):
        return f"{self.name} поет: Чирик!"

def animal_conversation(animals):
    """Функция, демонстрирующая полиморфизм"""
    for animal in animals:
        print(animal.speak())

# Создание животных
dog = Dog("Бобик")
cat = Cat("Мурка")
bird = Bird("Чижик")

animals = [dog, cat, bird]

# Демонстрация полиморфизма
animal_conversation(animals)
```

---

### Задание 7: Класс с магическими методами

Создайте класс `ComplexNumber`, который будет представлять комплексные числа и использовать магические методы для арифметических операций.

**Код для выполнения:**
```python
class ComplexNumber:
    """Класс для представления комплексных чисел"""
    
    def __init__(self, real, imag=0):
        self.real = real
        self.imag = imag
    
    def __str__(self):
        """Строковое представление комплексного числа"""
        if self.imag >= 0:
            return f"{self.real} + {self.imag}i"
        else:
            return f"{self.real} - {abs(self.imag)}i"
    
    def __repr__(self):
        """Представление для отладки"""
        return f"ComplexNumber({self.real}, {self.imag})"
    
    def __add__(self, other):
        """Сложение комплексных чисел"""
        return ComplexNumber(self.real + other.real, self.imag + other.imag)
    
    def __sub__(self, other):
        """Вычитание комплексных чисел"""
        return ComplexNumber(self.real - other.real, self.imag - other.imag)
    
    def __mul__(self, other):
        """Умножение комплексных чисел"""
        # (a + bi) * (c + di) = (ac - bd) + (ad + bc)i
        real_part = self.real * other.real - self.imag * other.imag
        imag_part = self.real * other.imag + self.imag * other.real
        return ComplexNumber(real_part, imag_part)
    
    def __eq__(self, other):
        """Сравнение комплексных чисел"""
        return self.real == other.real and self.imag == other.imag

# Пример использования
num1 = ComplexNumber(3, 4)
num2 = ComplexNumber(1, -2)

print(f"Число 1: {num1}")
print(f"Число 2: {num2}")
print(f"Сумма: {num1 + num2}")
print(f"Разность: {num1 - num2}")
print(f"Произведение: {num1 * num2}")
print(f"Равенство: {num1 == ComplexNumber(3, 4)}")
```

---

### Задание 8: Класс для работы со временем

Создайте класс `Time`, который будет представлять время в формате часы:минуты:секунды.

**Код для выполнения:**
```python
class Time:
    """Класс для представления времени"""
    
    def __init__(self, hours=0, minutes=0, seconds=0):
        """Инициализация времени с проверкой корректности"""
        # Нормализация времени
        total_seconds = hours * 3600 + minutes * 60 + seconds
        self.hours = (total_seconds // 3600) % 24
        self.minutes = (total_seconds % 3600) // 60
        self.seconds = total_seconds % 60
    
    def __str__(self):
        """Строковое представление времени"""
        return f"{self.hours:02d}:{self.minutes:02d}:{self.seconds:02d}"
    
    def __add__(self, other):
        """Сложение времени"""
        total_seconds = self.to_seconds() + other.to_seconds()
        hours = (total_seconds // 3600) % 24
        minutes = (total_seconds % 3600) // 60
        seconds = total_seconds % 60
        return Time(hours, minutes, seconds)
    
    def __sub__(self, other):
        """Вычитание времени"""
        total_seconds1 = self.to_seconds()
        total_seconds2 = other.to_seconds()
        diff_seconds = total_seconds1 - total_seconds2
        # Обработка отрицательного результата
        if diff_seconds < 0:
            diff_seconds = 0  # или можно сделать отрицательное время
        hours = (diff_seconds // 3600) % 24
        minutes = (diff_seconds % 3600) // 60
        seconds = diff_seconds % 60
        return Time(hours, minutes, seconds)
    
    def to_seconds(self):
        """Преобразование времени в секунды"""
        return self.hours * 3600 + self.minutes * 60 + self.seconds
    
    def is_after(self, other):
        """Проверяет, идет ли это время после другого"""
        return self.to_seconds() > other.to_seconds()

# Пример использования
time1 = Time(10, 30, 45)
time2 = Time(2, 15, 30)

print(f"Время 1: {time1}")
print(f"Время 2: {time2}")
print(f"Сумма: {time1 + time2}")
print(f"Разность: {time1 - time2}")
print(f"Время 1 позже времени 2: {time1.is_after(time2)}")
```

---

### Задание 9: Класс для работы с дробями

Создайте класс `Fraction`, который будет представлять обыкновенные дроби и выполнять арифметические операции с ними.

**Код для выполнения:**
```python
class Fraction:
    """Класс для представления обыкновенных дробей"""
    
    def __init__(self, numerator, denominator=1):
        """Инициализация дроби с сокращением"""
        if denominator == 0:
            raise ValueError("Знаменатель не может быть равен нулю")
        
        # Находим НОД для сокращения дроби
        gcd_val = self.gcd(abs(numerator), abs(denominator))
        self.numerator = numerator // gcd_val
        self.denominator = denominator // gcd_val
        
        # Приводим к положительному знаменателю
        if self.denominator < 0:
            self.numerator = -self.numerator
            self.denominator = -self.denominator
    
    def gcd(self, a, b):
        """Находит наибольший общий делитель"""
        while b:
            a, b = b, a % b
        return a
    
    def __str__(self):
        """Строковое представление дроби"""
        if self.denominator == 1:
            return str(self.numerator)
        return f"{self.numerator}/{self.denominator}"
    
    def __add__(self, other):
        """Сложение дробей"""
        new_num = self.numerator * other.denominator + other.numerator * self.denominator
        new_den = self.denominator * other.denominator
        return Fraction(new_num, new_den)
    
    def __sub__(self, other):
        """Вычитание дробей"""
        new_num = self.numerator * other.denominator - other.numerator * self.denominator
        new_den = self.denominator * other.denominator
        return Fraction(new_num, new_den)
    
    def __mul__(self, other):
        """Умножение дробей"""
        new_num = self.numerator * other.numerator
        new_den = self.denominator * other.denominator
        return Fraction(new_num, new_den)
    
    def __truediv__(self, other):
        """Деление дробей"""
        if other.numerator == 0:
            raise ZeroDivisionError("Деление на ноль")
        new_num = self.numerator * other.denominator
        new_den = self.denominator * other.numerator
        return Fraction(new_num, new_den)
    
    def __eq__(self, other):
        """Сравнение дробей"""
        return self.numerator == other.numerator and self.denominator == other.denominator

# Пример использования
frac1 = Fraction(1, 2)  # 1/2
frac2 = Fraction(1, 3)  # 1/3

print(f"Дробь 1: {frac1}")
print(f"Дробь 2: {frac2}")
print(f"Сумма: {frac1 + frac2}")
print(f"Разность: {frac1 - frac2}")
print(f"Произведение: {frac1 * frac2}")
print(f"Частное: {frac1 / frac2}")
print(f"Дроби равны: {frac1 == Fraction(2, 4)}")
```

---

### Задание 10: Комплексная задача - система управления библиотекой

Создайте классы для простой системы управления библиотекой: `Book`, `Member`, и `Library`.

**Код для выполнения:**
```python
from datetime import datetime, timedelta

class Book:
    """Класс для представления книги"""
    
    def __init__(self, isbn, title, author, year):
        self.isbn = isbn
        self.title = title
        self.author = author
        self.year = year
        self.is_available = True
        self.borrowed_by = None
        self.due_date = None
    
    def __str__(self):
        status = "доступна" if self.is_available else f"взята у {self.borrowed_by}"
        return f"{self.title} ({self.author}, {self.year}) - {status}"

class Member:
    """Класс для представления члена библиотеки"""
    
    def __init__(self, member_id, name, email):
        self.member_id = member_id
        self.name = name
        self.email = email
        self.borrowed_books = []
    
    def borrow_book(self, book):
        """Берет книгу из библиотеки"""
        if book.is_available:
            book.is_available = False
            book.borrowed_by = self.name
            book.due_date = datetime.now() + timedelta(days=14)  # 14 дней на возврат
            self.borrowed_books.append(book)
            return True
        return False
    
    def return_book(self, book):
        """Возвращает книгу в библиотеку"""
        if book in self.borrowed_books:
            book.is_available = True
            book.borrowed_by = None
            book.due_date = None
            self.borrowed_books.remove(book)
            return True
        return False

class Library:
    """Класс для представления библиотеки"""
    
    def __init__(self, name):
        self.name = name
        self.books = {}
        self.members = {}
    
    def add_book(self, book):
        """Добавляет книгу в библиотеку"""
        self.books[book.isbn] = book
    
    def register_member(self, member):
        """Регистрирует нового члена библиотеки"""
        self.members[member.member_id] = member
    
    def borrow_book(self, isbn, member_id):
        """Выдает книгу члену библиотеки"""
        if isbn not in self.books:
            return "Книга не найдена"
        
        if member_id not in self.members:
            return "Член библиотеки не найден"
        
        book = self.books[isbn]
        member = self.members[member_id]
        
        if book.is_available:
            if member.borrow_book(book):
                return f"Книга '{book.title}' выдана {member.name}"
            else:
                return "Не удалось выдать книгу"
        else:
            return f"Книга '{book.title}' уже взята"
    
    def return_book(self, isbn, member_id):
        """Принимает возврат книги от члена библиотеки"""
        if isbn not in self.books or member_id not in self.members:
            return "Книга или член библиотеки не найдены"
        
        book = self.books[isbn]
        member = self.members[member_id]
        
        if book in member.borrowed_books:
            if member.return_book(book):
                return f"Книга '{book.title}' возвращена"
            else:
                return "Не удалось вернуть книгу"
        else:
            return "Книга не была взята этим членом библиотеки"
    
    def get_overdue_books(self):
        """Возвращает список просроченных книг"""
        overdue = []
        current_date = datetime.now()
        
        for book in self.books.values():
            if not book.is_available and book.due_date < current_date:
                overdue.append({
                    'book': book,
                    'member_name': book.borrowed_by,
                    'days_overdue': (current_date - book.due_date).days
                })
        
        return overdue

# Пример использования
library = Library("Центральная библиотека")

# Добавляем книги
book1 = Book("978-0-123456-78-9", "Война и мир", "Лев Толстой", 1869)
book2 = Book("978-0-987654-32-1", "Преступление и наказание", "Федор Достоевский", 1866)
library.add_book(book1)
library.add_book(book2)

# Регистрируем членов библиотеки
member1 = Member("M001", "Иванов И.И.", "ivanov@example.com")
member2 = Member("M002", "Петрова П.П.", "petrova@example.com")
library.register_member(member1)
library.register_member(member2)

# Выдаем книги
print(library.borrow_book("978-0-123456-78-9", "M001"))
print(library.borrow_book("978-0-987654-32-1", "M002"))

# Возвращаем книгу
print(library.return_book("978-0-123456-78-9", "M001"))

# Проверяем просроченные книги
overdue_books = library.get_overdue_books()
if overdue_books:
    print("Просроченные книги:")
    for item in overdue_books:
        print(f"  {item['book'].title} - у {item['member_name']}, просрочено на {item['days_overdue']} дней")
else:
    print("Нет просроченных книг")
```

---

## Контрольные вопросы

1. Что такое класс в Python?
2. В чем разница между классом и объектом?
3. Что такое атрибуты и методы класса?
4. Какой метод является конструктором класса?
5. Что такое наследование и как его реализовать в Python?
6. В чем заключается полиморфизм в ООП?
7. Какие виды атрибутов существуют в Python (публичные, защищенные, приватные)?
8. Что такое магические методы и для чего они используются?
9. Как реализуется инкапсуляция в Python?
10. Что такое абстракция в контексте ООП?

## Вывод

В ходе этой практической работы были освоены основы объектно-ориентированного программирования в Python. Были рассмотрены ключевые концепции: классы, объекты, атрибуты, методы, конструкторы, наследование, инкапсуляция, полиморфизм и магические методы. ООП позволяет создавать более структурированный, читаемый и поддерживаемый код, особенно в крупных проектах.
