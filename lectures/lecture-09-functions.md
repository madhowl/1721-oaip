# Лекция 9: Функции

## Введение

Функции - это один из фундаментальных элементов программирования, позволяющий создавать переиспользуемый код, структурировать программу и улучшать её читаемость. В этой лекции мы подробно рассмотрим, как определять и использовать функции в Python, их параметры, возвращаемые значения, а также различные продвинутые концепции, такие как анонимные функции и области видимости.

## Основное содержание

### Что такое функции

**Функция** - это именованный блок кода, который может принимать параметры, выполнять определенные действия и возвращать результат. Функции позволяют разбивать сложные задачи на более мелкие, управляемые части, что делает код более понятным и поддерживаемым.

```python
# Простая функция без параметров
def greet():
    print("Привет, мир!")

# Вызов функции
greet()  # Вывод: Привет, мир!
```

### Определение функций

Функции в Python определяются с помощью ключевого слова `def`, за которым следует имя функции, круглые скобки и двоеточие:

```python
def имя_функции(параметры):
    """Документация функции (необязательно)"""
    # Тело функции
    return результат  # Необязательно
```

### Параметры функций

Функции могут принимать ноль или более параметров:

```python
# Функция с параметрами
def greet_user(name, greeting="Привет"):
    """Приветствует пользователя с заданным именем"""
    print(f"{greeting}, {name}!")

# Вызов функции
greet_user("Алексей")  # Привет, Алексей!
greet_user("Мария", "Добрый день")  # Добрый день, Мария!
```

#### Типы параметров:

1. **Обязательные параметры** - должны быть переданы при вызове функции
2. **Параметры по умолчанию** - имеют значение по умолчанию
3. **Параметры с переменным числом значений** (`*args`, `**kwargs`)

```python
# Пример функции с разными типами параметров
def example_function(required_param, default_param="значение по умолчанию", *args, **kwargs):
    print(f"Обязательный параметр: {required_param}")
    print(f"Параметр по умолчанию: {default_param}")
    print(f"Дополнительные позиционные аргументы: {args}")
    print(f"Дополнительные именованные аргументы: {kwargs}")

# Вызов функции
example_function("обязательный")
example_function("обязательный", "другое значение", 1, 2, 3, key1="value1", key2="value2")
```

### Возвращаемые значения

Функции могут возвращать значения с помощью ключевого слова `return`:

```python
# Функция с возвращаемым значением
def add_numbers(a, b):
    """Возвращает сумму двух чисел"""
    result = a + b
    return result

# Использование возвращаемого значения
sum_result = add_numbers(5, 3)
print(sum_result)  # 8

# Функция может возвращать несколько значений (на самом деле кортеж)
def divide_with_remainder(dividend, divisor):
    """Возвращает частное и остаток от деления"""
    quotient = dividend // divisor
    remainder = dividend % divisor
    return quotient, remainder

q, r = divide_with_remainder(17, 5)
print(f"Частное: {q}, остаток: {r}")  # Частное: 3, остаток: 2
```

### Области видимости переменных

В Python существуют разные области видимости переменных:

1. **Локальная область** - переменные внутри функции
2. **Глобальная область** - переменные на уровне модуля
3. **Встроенная область** - встроенные функции и переменные

```python
global_var = "Я глобальная переменная"

def example_scope():
    local_var = "Я локальная переменная"
    print(global_var)  # Доступ к глобальной переменной
    print(local_var)   # Доступ к локальной переменной

example_scope()
# print(local_var)  # Ошибка! local_var не доступна вне функции

# Изменение глобальной переменной изнутри функции
counter = 0

def increment():
    global counter  # Указывает, что мы хотим изменить глобальную переменную
    counter += 1

increment()
print(counter)  # 1
```

### Рекурсивные функции

Функция может вызывать саму себя, что называется рекурсией:

```python
# Пример рекурсивной функции для вычисления факториала
def factorial(n):
    """Вычисляет факториал числа n"""
    if n <= 1:
        return 1
    else:
        return n * factorial(n - 1)

print(factorial(5))  # 120

# Пример рекурсивной функции для вычисления чисел Фибоначчи
def fibonacci(n):
    """Возвращает n-е число Фибоначчи"""
    if n <= 1:
        return n
    else:
        return fibonacci(n - 1) + fibonacci(n - 2)

print(fibonacci(10))  # 55
```

### Анонимные функции (лямбда-функции)

Lambda-функции - это короткие анонимные функции, которые могут иметь любое количество аргументов, но содержать только одно выражение:

```python
# Пример лямбда-функции
square = lambda x: x ** 2
print(square(5))  # 25

# Лямбда-функции часто используются с map(), filter(), sorted()
numbers = [1, 2, 3, 4, 5]

# Удвоение чисел с помощью map и lambda
doubled = list(map(lambda x: x * 2, numbers))
print(doubled)  # [2, 4, 6, 8, 10]

# Фильтрация четных чисел
evens = list(filter(lambda x: x % 2 == 0, numbers))
print(evens)  # [2, 4]

# Сортировка по второму элементу кортежа
pairs = [(1, 'one'), (3, 'three'), (2, 'two')]
sorted_pairs = sorted(pairs, key=lambda pair: pair[1])
print(sorted_pairs)  # [(1, 'one'), (3, 'three'), (2, 'two')]
```

### Документирование функций

Хорошая практика - документировать функции с помощью docstring:

```python
def calculate_rectangle_area(length, width):
    """
    Вычисляет площадь прямоугольника.
    
    Args:
        length (float): Длина прямоугольника
        width (float): Ширина прямоугольника
    
    Returns:
        float: Площадь прямоугольника
    
    Raises:
        ValueError: Если длина или ширина отрицательны
    """
    if length < 0 or width < 0:
        raise ValueError("Длина и ширина должны быть неотрицательными")
    
    return length * width

# Доступ к документации
print(calculate_rectangle_area.__doc__)
```

### Функции высшего порядка

Функции в Python - это объекты первого класса, что означает, что их можно передавать как аргументы другим функциям:

```python
def apply_operation(x, y, operation):
    """Применяет операцию к двум аргументам"""
    return operation(x, y)

def multiply(a, b):
    return a * b

def power(a, b):
    return a ** b

# Использование функций как аргументов
result1 = apply_operation(5, 3, multiply)  # 15
result2 = apply_operation(2, 4, power)     # 16

print(result1, result2)  # 15 16
```

### Декораторы (введение)

Декораторы позволяют изменять поведение функций без изменения их кода:

```python
def my_decorator(func):
    """Простой декоратор, который добавляет вывод до и после вызова функции"""
    def wrapper(*args, **kwargs):
        print("Перед вызовом функции")
        result = func(*args, **kwargs)
        print("После вызова функции")
        return result
    return wrapper

@my_decorator
def say_hello(name):
    print(f"Привет, {name}!")

say_hello("Алексей")
# Вывод:
# Перед вызовом функции
# Привет, Алексей!
# После вызова функции
```

## Практические примеры

### Пример 1: Калькулятор с использованием функций

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

def calculator(num1, operator, num2):
    """Базовый калькулятор"""
    operations = {
        '+': add,
        '-': subtract,
        '*': multiply,
        '/': divide
    }
    
    if operator not in operations:
        raise ValueError(f"Неподдерживаемая операция: {operator}")
    
    return operations[operator](num1, num2)

# Использование калькулятора
print(calculator(10, '+', 5)) # 15
print(calculator(10, '*', 3))  # 30
```

### Пример 2: Работа со строками с использованием функций

```python
def count_vowels(text):
    """Подсчитывает количество гласных в тексте"""
    vowels = "аеёиоуыэюяАЕЁИОУЫЭЮЯaeiouAEIOU"
    count = 0
    for char in text:
        if char in vowels:
            count += 1
    return count

def reverse_words(text):
    """Переворачивает каждое слово в тексте"""
    words = text.split()
    reversed_words = [word[::-1] for word in words]
    return " ".join(reversed_words)

def clean_text(text):
    """Очищает текст от лишних пробелов и переводов строк"""
    import re
    # Удаляет лишние пробелы и переводы строк
    cleaned = re.sub(r'\s+', ' ', text.strip())
    return cleaned

# Примеры использования
text = "  Привет,   мир! Как дела?  "
print(f"Количество гласных: {count_vowels(text)}")
print(f"Перевернутые слова: {reverse_words(text)}")
print(f"Очищенный текст: '{clean_text(text)}'")
```

### Пример 3: Работа со списками с использованием функций

```python
def find_max_min(numbers):
    """Находит максимальное и минимальное значение в списке"""
    if not numbers:
        return None, None
    
    max_val = min_val = numbers[0]
    for num in numbers[1:]:
        if num > max_val:
            max_val = num
        elif num < min_val:
            min_val = num
    
    return max_val, min_val

def remove_duplicates(lst):
    """Удаляет дубликаты из списка, сохраня порядок"""
    seen = set()
    result = []
    for item in lst:
        if item not in seen:
            seen.add(item)
            result.append(item)
    return result

def bubble_sort(arr):
    """Сортировка пузырьком"""
    n = len(arr)
    arr = arr.copy()  # Создаем копию, чтобы не изменять оригинал
    
    for i in range(n):
        for j in range(0, n - i - 1):
            if arr[j] > arr[j + 1]:
                arr[j], arr[j + 1] = arr[j + 1], arr[j]
    
    return arr

# Примеры использования
numbers = [3, 1, 4, 1, 5, 9, 2, 6, 5, 3, 5]
max_val, min_val = find_max_min(numbers)
print(f"Максимум: {max_val}, Минимум: {min_val}")

list_with_dups = [1, 2, 2, 3, 4, 4, 5]
unique_list = remove_duplicates(list_with_dups)
print(f"Без дубликатов: {unique_list}")

unsorted = [64, 34, 25, 12, 22, 11, 90]
sorted_list = bubble_sort(unsorted)
print(f"Отсортированный список: {sorted_list}")
```

## Заключение

В этой лекции мы подробно рассмотрели функции в Python:

1. **Определение функций** с помощью ключевого слова `def`
2. **Параметры функций** - обязательные, по умолчанию, переменное число
3. **Возвращаемые значения** и ключевое слово `return`
4. **Области видимости переменных** - локальные и глобальные
5. **Рекурсивные функции** для решения задач рекурсивным способом
6. **Анонимные функции (лямбда-функции)** для коротких операций
7. **Документирование функций** с помощью docstring
8. **Функции высшего порядка** - функции, принимающие другие функции
9. **Введение в декораторы** для изменения поведения функций

Функции являются важнейшим инструментом для структурирования кода, повышения его читаемости и переиспользуемости. В следующей лекции мы рассмотрим модули и библиотеки в Python.
