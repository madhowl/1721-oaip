# Практическая работа 9: Написание и использование функций

## Цель работы

Научиться создавать и использовать функции в Python, освоить основные концепции функционального программирования: параметры, возвращаемые значения, области видимости, рекурсия, а также понять, как использовать функции для структурирования кода и повторного использования кода.

## Теоретическая часть

Функция в Python - это блок кода, который можно вызывать с определенными аргументами и который может возвращать значение. Функции позволяют структурировать код, избежать дублирования и сделать программу более читаемой и поддерживаемой.

```python
# Пример простой функции
def greet(name):
    """Приветствует пользователя по имени"""
    return f"Привет, {name}!"

# Вызов функции
message = greet("Алексей")
print(message)  # Привет, Алексей!
```

### Основные элементы функции:
- Ключевое слово `def`
- Имя функции
- Параметры в круглых скобках
- Двоеточие
- Тело функции (с отступом)
- Опциональный оператор `return`

## Практические задания

### Задание 1: Создание простой функции

Создайте функцию, которая принимает два числа и возвращает их сумму. Добавьте документацию к функции и вызовите её с разными параметрами.

**Пример выполнения:**
```
Сумма 5 и 3: 8
Сумма 10 и 20: 30
```

**Код для выполнения:**
```python
def add_numbers(a, b):
    """
    Возвращает сумму двух чисел
    
    Args:
        a (int/float): Первое число
        b (int/float): Второе число
    
    Returns:
        int/float: Сумма чисел a и b
    """
    return a + b

# Примеры использования
result1 = add_numbers(5, 3)
result2 = add_numbers(10, 20)

print(f"Сумма 5 и 3: {result1}")
print(f"Сумма 10 и 20: {result2}")
```

---

### Задание 2: Функция с параметрами по умолчанию

Создайте функцию, которая вычисляет площадь прямоугольника. Установите значение по умолчанию для одного из параметров (например, ширины).

**Пример выполнения:**
```
Площадь (5x3): 15
Площадь (5x1): 5
```

**Код для выполнения:**
```python
def calculate_rectangle_area(length, width=1):
    """
    Вычисляет площадь прямоугольника
    
    Args:
        length (float): Длина прямоугольника
        width (float): Ширина прямоугольника (по умолчанию 1)
    
    Returns:
        float: Площадь прямоугольника
    """
    return length * width

# Примеры использования
area1 = calculate_rectangle_area(5, 3)
area2 = calculate_rectangle_area(5)  # ширина по умолчанию

print(f"Площадь (5x3): {area1}")
print(f"Площадь (5x1): {area2}")
```

---

### Задание 3: Функция с переменным числом аргументов

Создайте функцию, которая принимает произвольное количество чисел и возвращает их сумму и среднее значение.

**Пример выполнения:**
```
Введите числа через пробел: 1 2 3 4 5
Сумма: 15
Среднее: 3.0
```

**Код для выполнения:**
```python
def calculate_sum_and_average(*args):
    """
    Возвращает сумму и среднее значение произвольного количества чисел
    
    Args:
        *args: Произвольное количество чисел
    
    Returns:
        tuple: (сумма, среднее значение)
    """
    if not args:
        return 0, 0
    
    total = sum(args)
    average = total / len(args)
    return total, average

# Пример использования
numbers_str = input("Введите числа через пробел: ")
numbers = [float(x) for x in numbers_str.split()]

total, average = calculate_sum_and_average(*numbers)
print(f"Сумма: {total}")
print(f"Среднее: {average}")
```

---

### Задание 4: Функция с именованными аргументами

Создайте функцию, которая принимает информацию о человеке (имя, возраст, город) и возвращает отформатированную строку. Используйте именованные аргументы.

**Пример выполнения:**
```
Информация о пользователе: Иван Иванов, 25 лет, Москва
```

**Код для выполнения:**
```python
def format_person_info(name, age, city):
    """
    Форматирует информацию о человеке
    
    Args:
        name (str): Имя человека
        age (int): Возраст
        city (str): Город проживания
    
    Returns:
        str: Отформатированная строка с информацией
    """
    return f"{name}, {age} лет, {city}"

# Пример использования с именованными аргументами
info = format_person_info(name="Иван Иванов", age=25, city="Москва")
print(f"Информация о пользователе: {info}")
```

---

### Задание 5: Рекурсивная функция

Создайте рекурсивную функцию для вычисления факториала числа.

**Пример выполнения:**
```
Факториал 5: 120
Факториал 0: 1
```

**Код для выполнения:**
```python
def factorial(n):
    """
    Вычисляет факториал числа рекурсивно
    
    Args:
        n (int): Число для вычисления факториала (должно быть >= 0)
    
    Returns:
        int: Факториал числа n
    """
    if n < 0:
        raise ValueError("Факториал определен только для неотрицательных чисел")
    if n == 0 or n == 1:
        return 1
    return n * factorial(n - 1)

# Примеры использования
print(f"Факториал 5: {factorial(5)}")
print(f"Факториал 0: {factorial(0)}")
```

---

### Задание 6: Функция с возвращаемым словарем

Создайте функцию, которая принимает строку и возвращает словарь с информацией о строке: длина, количество слов, количество гласных и согласных.

**Пример выполнения:**
```
Информация о строке 'Привет мир':
Длина: 10
Количество слов: 2
Гласных: 3
Согласных: 5
```

**Код для выполнения:**
```python
def analyze_string(text):
    """
    Анализирует строку и возвращает информацию о ней
    
    Args:
        text (str): Входная строка для анализа
    
    Returns:
        dict: Словарь с информацией о строке
    """
    vowels = "аеёиоуыэюяaeiouAEIOU"
    consonants = "бвгджзйклмнпрстфхцчшщbcdfghjklmnpqrstvwxyz"
    
    # Подсчет гласных и согласных
    vowel_count = 0
    consonant_count = 0
    
    for char in text:
        if char in vowels:
            vowel_count += 1
        elif char in consonants:
            consonant_count += 1
    
    # Подсчет слов
    words = text.split()
    word_count = len(words)
    
    return {
        "length": len(text),
        "word_count": word_count,
        "vowel_count": vowel_count,
        "consonant_count": consonant_count
    }

# Пример использования
text = "Привет мир"
analysis = analyze_string(text)

print(f"Информация о строке '{text}':")
for key, value in analysis.items():
    print(f"{key.replace('_', ' ').title()}: {value}")
```

---

### Задание 7: Использование лямбда-функций

Создайте программу, которая использует лямбда-функции для выполнения математических операций и работы с коллекциями.

**Пример выполнения:**
```
Квадраты: [1, 4, 9, 16, 25]
Четные числа: [2, 4]
Сумма: 15
```

**Код для выполнения:**
```python
# Лямбда-функции для математических операций
add = lambda x, y: x + y
multiply = lambda x, y: x * y
square = lambda x: x ** 2

# Использование лямбда-функций с map(), filter(), reduce()
numbers = [1, 2, 3, 4, 5]

# Возведение в квадрат
squares = list(map(square, numbers))
print(f"Квадраты: {squares}")

# Фильтрация четных чисел
evens = list(filter(lambda x: x % 2 == 0, numbers))
print(f"Четные числа: {evens}")

# Сумма чисел
from functools import reduce
total = reduce(lambda x, y: x + y, numbers)
print(f"Сумма: {total}")
```

---

### Задание 8: Функции высшего порядка

Создайте функцию высшего порядка, которая принимает другую функцию и список значений, а затем применяет функцию к каждому элементу списка.

**Пример выполнения:**
```
Оригинальные числа: [1, 2, 3, 4, 5]
Удвоенные числа: [2, 4, 6, 8, 10]
Квадраты чисел: [1, 4, 9, 16, 25]
```

**Код для выполнения:**
```python
def apply_function_to_list(func, values):
    """
    Применяет функцию к каждому элементу списка
    
    Args:
        func (function): Функция для применения
        values (list): Список значений
    
    Returns:
        list: Список результатов применения функции
    """
    return [func(x) for x in values]

# Определяем несколько функций для применения
def double(x):
    return x * 2

def square(x):
    return x ** 2

def is_positive(x):
    return x > 0

# Примеры использования
numbers = [1, 2, 3, 4, 5]

doubled = apply_function_to_list(double, numbers)
squared = apply_function_to_list(square, numbers)

print(f"Оригинальные числа: {numbers}")
print(f"Удвоенные числа: {doubled}")
print(f"Квадраты чисел: {squared}")
```

---

### Задание 9: Функция с внутренними функциями

Создайте функцию, которая содержит внутреннюю функцию для выполнения вспомогательной операции.

**Пример выполнения:**
```
Площадь прямоугольника: 20
Площадь круга: 78.54
Площадь треугольника: 24.0
```

**Код для выполнения:**
```python
def calculate_area(shape, *dimensions):
    """
    Вычисляет площадь различных фигур
    
    Args:
        shape (str): Тип фигуры ('rectangle', 'circle', 'triangle')
        *dimensions: Параметры фигуры
    
    Returns:
        float: Площадь фигуры
    """
    def rectangle_area(length, width):
        return length * width
    
    def circle_area(radius):
        return 3.14159 * radius ** 2
    
    def triangle_area(base, height):
        return 0.5 * base * height
    
    if shape == "rectangle":
        return rectangle_area(*dimensions)
    elif shape == "circle":
        return circle_area(*dimensions)
    elif shape == "triangle":
        return triangle_area(*dimensions)
    else:
        raise ValueError(f"Неизвестная фигура: {shape}")

# Примеры использования
area1 = calculate_area("rectangle", 5, 4)  # 20
area2 = calculate_area("circle", 5)       # 78.53975
area3 = calculate_area("triangle", 6, 8)  # 24

print(f"Площадь прямоугольника: {area1}")
print(f"Площадь круга: {area2:.2f}")
print(f"Площадь треугольника: {area3}")
```

---

### Задание 10: Декораторы (ознакомительное)

Создайте простой декоратор, который измеряет время выполнения функции.

**Пример выполнения:**
```
Функция выполнена за 0.000123 секунд
```

**Код для выполнения:**
```python
import time

def timer_decorator(func):
    """
    Декоратор для измерения времени выполнения функции
    """
    def wrapper(*args, **kwargs):
        start_time = time.time()
        result = func(*args, **kwargs)
        end_time = time.time()
        print(f"Функция {func.__name__} выполнена за {end_time - start_time:.6f} секунд")
        return result
    return wrapper

@timer_decorator
def slow_function():
    """Функция, которая имитирует длительное выполнение"""
    time.sleep(0.1)  # Задержка 0.1 секунды
    return "Готово!"

# Пример использования
result = slow_function()
print(result)
```

---

### Задание 11: Функции для конвертации единиц

Создайте набор функций для конвертации различных единиц измерения (температура, длина, масса).

**Пример выполнения:**
```
25°C = 77.0°F
100°F = 37.78°C
5 км = 3.11 миль
```

**Код для выполнения:**
```python
def celsius_to_fahrenheit(celsius):
    """Конвертирует температуру из Цельсия в Фаренгейт"""
    return celsius * 9/5 + 32

def fahrenheit_to_celsius(fahrenheit):
    """Конвертирует температуру из Фаренгейта в Цельсия"""
    return (fahrenheit - 32) * 5/9

def km_to_miles(kilometers):
    """Конвертирует километры в мили"""
    return kilometers * 0.621371

def miles_to_km(miles):
    """Конвертирует мили в километры"""
    return miles / 0.621371

def kg_to_pounds(kilograms):
    """Конвертирует килограммы в фунты"""
    return kilograms * 2.20462

def pounds_to_kg(pounds):
    """Конвертирует фунты в килограммы"""
    return pounds / 2.20462

# Примеры использования
temp_c = 25
temp_f = celsius_to_fahrenheit(temp_c)
print(f"{temp_c}°C = {temp_f}°F")

distance_km = 5
distance_miles = km_to_miles(distance_km)
print(f"{distance_km} км = {distance_miles:.2f} миль")
```

---

### Задание 12: Функция для расчета площадей

Создайте функции для расчета площадей различных геометрических фигур: круга, прямоугольника, треугольника, трапеции.

**Пример выполнения:**
```
Площадь круга радиусом 5: 78.54
Площадь прямоугольника 4x6: 24
Площадь треугольника с основанием 6 и высотой 8: 24.0
```

**Код для выполнения:**
```python
import math

def circle_area(radius):
    """Вычисляет площадь круга"""
    return math.pi * radius ** 2

def rectangle_area(length, width):
    """Вычисляет площадь прямоугольника"""
    return length * width

def triangle_area(base, height):
    """Вычисляет площадь треугольника"""
    return 0.5 * base * height

def trapezoid_area(base1, base2, height):
    """Вычисляет площадь трапеции"""
    return 0.5 * (base1 + base2) * height

def parallelogram_area(base, height):
    """Вычисляет площадь параллелограмма"""
    return base * height

# Примеры использования
print(f"Площадь круга радиусом 5: {circle_area(5):.2f}")
print(f"Площадь прямоугольника 4x6: {rectangle_area(4, 6)}")
print(f"Площадь треугольника с основанием 6 и высотой 8: {triangle_area(6, 8)}")
print(f"Площадь трапеции с основаниями 5 и 7, высотой 4: {trapezoid_area(5, 7, 4)}")
```

---

### Задание 13: Функция с обработкой исключений

Создайте функцию, которая безопасно выполняет деление и обрабатывает возможные исключения.

**Пример выполнения:**
```
Результат деления 10 на 2: 5.0
Ошибка: деление на ноль
```

**Код для выполнения:**
```python
def safe_divide(a, b):
    """
    Безопасно делит два числа с обработкой исключений
    
    Args:
        a (float): Делимое
        b (float): Делитель
    
    Returns:
        float or None: Результат деления или None в случае ошибки
    """
    try:
        if not isinstance(a, (int, float)) or not isinstance(b, (int, float)):
            raise TypeError("Аргументы должны быть числами")
        
        result = a / b
        return result
    except ZeroDivisionError:
        print("Ошибка: деление на ноль")
        return None
    except TypeError as e:
        print(f"Ошибка типа данных: {e}")
        return None

# Примеры использования
print(f"Результат деления 10 на 2: {safe_divide(10, 2)}")
print(f"Результат деления 10 на 0: {safe_divide(10, 0)}")
print(f"Результат деления 'десять' на 2: {safe_divide('десять', 2)}")
```

---

### Задание 14: Функция для работы с последовательностями

Создайте функции для обработки последовательностей: нахождение максимума, минимума, среднего, медианы.

**Код для выполнения:**
```python
def find_max(seq):
    """Находит максимальное значение в последовательности"""
    if not seq:
        return None
    max_val = seq[0]
    for item in seq[1:]:
        if item > max_val:
            max_val = item
    return max_val

def find_min(seq):
    """Находит минимальное значение в последовательности"""
    if not seq:
        return None
    min_val = seq[0]
    for item in seq[1:]:
        if item < min_val:
            min_val = item
    return min_val

def calculate_average(seq):
    """Вычисляет среднее значение последовательности"""
    if not seq:
        return 0
    return sum(seq) / len(seq)

def calculate_median(seq):
    """Вычисляет медиану последовательности"""
    if not seq:
        return None
    
    sorted_seq = sorted(seq)
    n = len(sorted_seq)
    
    if n % 2 == 0:
        # Если четное количество элементов, медиана - среднее двух центральных
        return (sorted_seq[n//2 - 1] + sorted_seq[n//2]) / 2
    else:
        # Если нечетное количество элементов, медиана - центральный элемент
        return sorted_seq[n//2]

# Примеры использования
numbers = [3, 1, 4, 1, 5, 9, 2, 6, 5, 3, 5]

print(f"Последовательность: {numbers}")
print(f"Максимум: {find_max(numbers)}")
print(f"Минимум: {find_min(numbers)}")
print(f"Среднее: {calculate_average(numbers):.2f}")
print(f"Медиана: {calculate_median(numbers)}")
```

---

### Задание 15: Комплексная задача - калькулятор с функциями

Создайте программу калькулятора, которая использует отдельные функции для каждой операции и организована в виде модульной структуры.

**Код для выполнения:**
```python
def add(a, b):
    """Сложение двух чисел"""
    return a + b

def subtract(a, b):
    """Вычитание двух чисел"""
    return a - b

def multiply(a, b):
    """Умножение двух чисел"""
    return a * b

def divide(a, b):
    """Деление двух чисел"""
    if b == 0:
        raise ZeroDivisionError("Деление на ноль невозможно")
    return a / b

def power(a, b):
    """Возведение в степень"""
    return a ** b

def calculate(operation, a, b):
    """Выполняет операцию над двумя числами"""
    operations = {
        '+': add,
        '-': subtract,
        '*': multiply,
        '/': divide,
        '**': power,
        '^': power
    }
    
    if operation not in operations:
        raise ValueError(f"Неподдерживаемая операция: {operation}")
    
    return operations[operation](a, b)

def calculator():
    """Основная функция калькулятора"""
    print("Калькулятор. Поддерживаемые операции: +, -, *, /, **")
    print("Для выхода введите 'quit'")
    
    while True:
        try:
            expr = input("\nВведите выражение (например, '5 + 3'): ")
            
            if expr.lower() == 'quit':
                break
            
            parts = expr.split()
            if len(parts) != 3:
                print("Неверный формат. Используйте формат: число операция число")
                continue
            
            a = float(parts[0])
            op = parts[1]
            b = float(parts[2])
            
            result = calculate(op, a, b)
            print(f"Результат: {a} {op} {b} = {result}")
            
        except ValueError as e:
            print(f"Ошибка ввода: {e}")
        except ZeroDivisionError as e:
            print(f"Ошибка: {e}")
        except Exception as e:
            print(f"Неизвестная ошибка: {e}")

# Запуск калькулятора (закомментирован для предотвращения бесконечного цикла при проверке)
# calculator()
```

---

## Контрольные вопросы

1. Как объявить функцию в Python?
2. В чем разница между параметрами и аргументами функции?
3. Как вернуть значение из функции?
4. Что такое параметры по умолчанию и как их использовать?
5. Как передать переменное количество аргументов в функцию?
6. Что такое лямбда-функция и где она используется?
7. Как использовать функции map(), filter(), reduce()?
8. Что такое область видимости переменных в функциях?
9. Что такое рекурсивная функция?
10. Какие преимущества дает использование функций в программировании?

## Вывод

В ходе этой практической работы были освоены основы работы с функциями в Python:
- Создание и вызов функций
- Использование различных типов параметров
- Возврат значений из функций
- Применение лямбда-функций
- Использование функций высшего порядка
- Применение функций для решения задач вычисления и анализа данных

Функции позволяют структурировать код, делают его более читаемым и переиспользуемым. Понимание работы с функциями является важным шагом на пути к профессиональному программированию.
