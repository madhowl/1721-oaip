# Практическая работа 9: Написание и использование функций

## Цель работы

Научиться создавать и использовать функции в Python, освоить различные типы параметров, возвращаемые значения, а также анонимные функции (лямбда-выражения) и их применение в различных задачах.

## Теоретическая часть

Функция - это именованный блок кода, который может принимать параметры и возвращать значение. Функции позволяют структурировать код, избежать дублирования и улучшить читаемость программы.

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
Сумма: 15
Квадраты: [1, 4, 9, 16, 25]
Четные числа: [2, 4]
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
Результат: 100
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
print(f"Площадь круга: {area2}")
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

## Дополнительные задания

### Задание 11: Калькулятор с использованием функций

Создайте программу калькулятора, которая использует отдельные функции для каждой операции.

**Код для выполнения:**
```python
def add(a, b):
    return a + b

def subtract(a, b):
    return a - b

def multiply(a, b):
    return a * b

def divide(a, b):
    if b == 0:
        raise ZeroDivisionError("Деление на ноль невозможно")
    return a / b

def calculator():
    """Простой калькулятор с использованием функций"""
    print("Калькулятор. Поддерживаемые операции: +, -, *, /")
    
    while True:
        try:
            num1 = float(input("Введите первое число (или 'q' для выхода): "))
            operator = input("Введите операцию (+, -, *, /): ")
            num2 = float(input("Введите второе число: "))
            
            if operator == '+':
                result = add(num1, num2)
            elif operator == '-':
                result = subtract(num1, num2)
            elif operator == '*':
                result = multiply(num1, num2)
            elif operator == '/':
                result = divide(num1, num2)
            else:
                print("Неподдерживаемая операция")
                continue
            
            print(f"Результат: {num1} {operator} {num2} = {result}")
            
        except ValueError:
            print("Неверный ввод числа")
        except ZeroDivisionError as e:
            print(f"Ошибка: {e}")
        except KeyboardInterrupt:
            print("\nПрограмма завершена пользователем")
            break

# Запуск калькулятора (закомментировано для предотвращения бесконечного цикла при проверке)
# calculator()
```

---

### Задание 12: Работа со строками с использованием функций

Создайте набор функций для обработки строк: подсчет слов, подсчет символов, проверка на палиндром.

**Код для выполнения:**
```python
def count_words(text):
    """Подсчитывает количество слов в тексте"""
    return len(text.split())

def count_characters(text, exclude_spaces=True):
    """Подсчитывает количество символов в тексте"""
    if exclude_spaces:
        text = text.replace(" ", "")
    return len(text)

def is_palindrome(text):
    """Проверяет, является ли текст палиндромом"""
    cleaned = ''.join(char.lower() for char in text if char.isalnum())
    return cleaned == cleaned[::-1]

def text_statistics(text):
    """Возвращает статистику по тексту"""
    return {
        "words": count_words(text),
        "characters": count_characters(text),
        "characters_no_spaces": count_characters(text, exclude_spaces=True),
        "is_palindrome": is_palindrome(text)
    }

# Пример использования
text = "А роза упала на лапу Азора"
stats = text_statistics(text)

print(f"Текст: '{text}'")
print(f"Количество слов: {stats['words']}")
print(f"Количество символов (с пробелами): {stats['characters']}")
print(f"Количество символов (без пробелов): {stats['characters_no_spaces']}")
print(f"Является палиндромом: {stats['is_palindrome']}")
```

---

## Контрольные вопросы

1. Что такое функция в Python?
2. Как объявить функцию?
3. В чем разница между параметрами и аргументами?
4. Как вернуть значение из функции?
5. Что такое параметры по умолчанию?
6. Как передать переменное число аргументов в функцию?
7. Что такое лямбда-функция?
8. В чем разница между `map()`, `filter()` и `reduce()`?
9. Что такое функция высшего порядка?
10. Для чего нужны декораторы?

## Вывод

В ходе этой практической работы были освоены основы работы с функциями в Python:
- Создание и вызов функций
- Использование различных типов параметров
- Возврат значений из функций
- Применение лямбда-функций
- Использование функций высшего порядка
- Применение функций для решения задач обработки данных

Функции позволяют структурировать код, делают его более читаемым и переиспользуемым. Понимание работы с функциями является важным шагом на пути к профессиональному программированию.
