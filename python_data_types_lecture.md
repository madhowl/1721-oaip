# Лекция: Типы данных и переменные в Python

## Введение

Python — это язык программирования с динамической типизацией, что означает, что тип переменной определяется автоматически во время выполнения программы. В этой лекции мы рассмотрим основные типы данных и работу с переменными в Python.

## Переменные

Переменная — это имя, которое связано со значением в памяти компьютера. В Python создание переменной происходит при присваивании значения с помощью оператора `=`.

```python
age = 25
name = "Алексей"
is_student = True
```

Важно понимать, что в Python переменные не имеют фиксированного типа — они могут ссылаться на значения разных типов в разное время:

```python
x = 10      # x теперь целое число
x = "text"  # x теперь строка
```

## Основные типы данных

### 1. Числовые типы

#### Целые числа (`int`)

Целые числа — это числа без дробной части. В Python целые числа могут быть произвольной длины (ограничены только доступной памятью).

```python
positive_int = 42
negative_int = -17
zero = 0
big_number = 999999999999
```

Операции с целыми числами:
- Сложение: `+`
- Вычитание: `-`
- Умножение: `*`
- Деление: `/` (возвращает float)
- Целочисленное деление: `//`
- Остаток от деления: `%`
- Возведение в степень: `**`

Примеры:
```python
a = 8
b = 3

print(a + b)   # 1
print(a - b)   # 5
print(a * b)   # 24
print(a / b)   # 2.66666666665
print(a // b)  # 2
print(a % b)   # 2
print(a ** b)  # 512
```

#### Числа с плавающей точкой (`float`)

Тип `float` представляет вещественные числа (числа с десятичной точкой).

```python
pi = 3.14159
temperature = -5.5
scientific_notation = 1.23e-4  # 0.00123
```

Операции с float аналогичны операциям с int, но результат может содержать погрешности из-за особенностей представления вещественных чисел в компьютере:

```python
x = 0.1
y = 0.2
print(x + y)  # 0.300000004
```

Это важный момент при работе с финансовыми данными или когда требуется высокая точность.

### 2. Строки (`str`)

Строки — это последовательности символов, заключенные в кавычки (одинарные, двойные или тройные).

```python
single_quotes = 'Привет'
double_quotes = "Мир"
triple_quotes = """Это многострочная
строка"""
```

Операции со строками:
- Конкатенация: `+`
- Повторение: `*`
- Доступ к символу: `[]`
- Срезы: `[start:end]`
- Длина строки: `len()`

Примеры:
```python
first_name = "Иван"
last_name = "Петров"

full_name = first_name + " " + last_name  # "Иван Петров"
greeting = "Привет, " * 2                 # "Привет, Привет, "

message = "Python"
print(message[0])      # "P"
print(message[-1])     # "n"
print(message[1:4])    # "yth"
print(len(message))    # 6
```

#### Методы строк

Строки в Python имеют множество встроенных методов:

```python
text = "  Hello World  "
print(text.upper())        # "  HELLO WORLD  "
print(text.lower())        # "  hello world  "
print(text.strip())        # "Hello World"
print(text.replace("o", "0"))  # " Hell0 W0rld  "
print(text.split())        # ['Hello', 'World']
```

### 3. Логический тип (`bool`)

Логический тип может принимать только два значения: `True` и `False`.

```python
is_sunny = True
is_raining = False
```

Логические значения обычно получаются в результате сравнений:

```python
age = 18
can_vote = age >= 18      # True
is_minor = age < 18       # False
is_equal = 5 == 5         # True
is_not_equal = 5 != 3     # True
```

Логические операции:
- И: `and`
- ИЛИ: `or`
- НЕ: `not`

Примеры:
```python
age = 25
has_license = True

can_drive = age >= 18 and has_license  # True
is_teen_or_adult = 13 <= age <= 19 or age >= 20  # True
is_not_student = not True  # False
```

## Преобразование типов

Иногда необходимо преобразовать значение одного типа в другой. Python предоставляет встроенные функции для этого:

### Явное преобразование

```python
# В int
float_to_int = int(3.7)      # 3 (дробная часть отбрасывается)
string_to_int = int("123")   # 123

# В float
int_to_float = float(42)     # 42.0
string_to_float = float("3.14") # 3.14

# В str
int_to_str = str(42)         # "42"
float_to_str = str(3.14)     # "3.14"
bool_to_str = str(True)      # "True"

# В bool
int_to_bool = bool(1)        # True
zero_to_bool = bool(0)       # False
empty_string_to_bool = bool("")  # False
non_empty_to_bool = bool("text") # True
```

### Неявное преобразование

В некоторых выражениях Python автоматически преобразует типы:

```python
result = 5 + 3.2    # 8.2 (int преобразуется в float)
print(type(result)) # <class 'float'>
```

### Особенности преобразования

При преобразовании строк в числа нужно быть осторожным:

```python
valid_conversion = int("123")    # Работает
# invalid_conversion = int("abc")  # Вызовет ошибку ValueError
```

Для безопасного преобразования можно использовать конструкцию `try-except`:

```python
def safe_int_convert(value):
    try:
        return int(value)
    except ValueError:
        return None

print(safe_int_convert("123"))  # 123
print(safe_int_convert("abc"))  # None
```

## Практические примеры

### Пример 1: Калькулятор средней скорости

```python
distance = 150.5  # километры
time = 2.5        # часы

speed = distance / time
print(f"Средняя скорость: {speed} км/ч")
```

### Пример 2: Проверка возраста

```python
birth_year = int(input("Введите год рождения: "))
current_year = 2023
age = current_year - birth_year

is_adult = age >= 18
print(f"Вам {age} лет")
print(f"Вы совершеннолетний: {is_adult}")
```

### Пример 3: Обработка текста

```python
user_input = input("Введите ваше имя: ").strip().title()
greeting = f"Привет, {user_input}!"
print(greeting)
print(f"Длина вашего имени: {len(user_input)} символов")
```

## Заключение

В этой лекции мы рассмотрели основные типы данных в Python:
- Числовые типы (int, float)
- Строки (str)
- Логический тип (bool)

Мы также изучили операции, которые можно выполнять с этими типами, и способы преобразования между ними. Понимание этих концепций является фундаментом для дальнейшего изучения Python.
