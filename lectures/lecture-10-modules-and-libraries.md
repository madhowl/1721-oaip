# Лекция 10: Модули и библиотеки

## Введение

Модули и библиотеки являются важной частью экосистемы Python, позволяя повторно использовать код, расширять функциональность программ и организовывать проекты более структурированно. В этой лекции мы рассмотрим, как работать с модулями, какие стандартные библиотеки доступны в Python, и как использовать сторонние библиотеки.

## Основное содержание

### Что такое модули

**Модуль** - это файл, содержащий определения и инструкции на Python. Имя файла - это имя модуля с добавлением суффикса `.py`. Модуль может содержать исполняемый код, а также определения функций, классов и переменных.

```python
# Пример модуля my_module.py
def greet(name):
    """Приветствует пользователя"""
    return f"Привет, {name}!"

def calculate_square_area(side):
    """Вычисляет площадь квадрата"""
    return side ** 2

PI = 3.14159
```

### Импорт модулей

Python предоставляет несколько способов импорта модулей:

#### Импорт всего модуля

```python
import math
import os
import sys

# Использование функций из модуля
result = math.sqrt(16)
print(result)  # 4.0

# Использование констант из модуля
print(math.pi)  # 3.141592653589793
```

#### Импорт с псевдонимом

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt

# Использование модуля с псевдонимом
array = np.array([1, 2, 3, 4])
print(array)  # [1 2 3 4]
```

#### Импорт конкретных элементов

```python
from math import sqrt, pi, sin, cos
from os import getcwd, listdir
from random import randint, choice

# Использование импортированных элементов напрямую
result = sqrt(25)  # 5.0
print(pi)  # 3.141592653589793
random_num = randint(1, 10)
```

#### Импорт всех элементов (не рекомендуется)

```python
from math import *

# Теперь все функции и константы из math доступны напрямую
result = sqrt(16)
print(sin(pi/2))  # 1.0

# Однако это может привести к конфликтам имен
```

### Создание и использование собственных модулей

Предположим, у нас есть файл `geometry.py`:

```python
# geometry.py
def calculate_circle_area(radius):
    """Вычисляет площадь круга"""
    from math import pi
    return pi * radius ** 2

def calculate_triangle_area(base, height):
    """Вычисляет площадь треугольника"""
    return 0.5 * base * height

def calculate_rectangle_area(length, width):
    """Вычисляет площадь прямоугольника"""
    return length * width

# Константы
EARTH_RADIUS_KM = 6371
```

Теперь мы можем использовать этот модуль в другом файле:

```python
# main.py
import geometry

# Использование функций из нашего модуля
circle_area = geometry.calculate_circle_area(5)
triangle_area = geometry.calculate_triangle_area(10, 8)
rectangle_area = geometry.calculate_rectangle_area(6, 4)

print(f"Площадь круга: {circle_area}")
print(f"Площадь треугольника: {triangle_area}")
print(f"Площадь прямоугольника: {rectangle_area}")
print(f"Радиус Земли: {geometry.EARTH_RADIUS_KM} км")
```

### Стандартная библиотека Python

Python поставляется с богатой стандартной библиотекой, которая включает в себя множество модулей для различных задач:

#### Модуль `os` - работа с операционной системой

```python
import os

# Получение текущей директории
current_dir = os.getcwd()
print(f"Текущая директория: {current_dir}")

# Список файлов в директории
files = os.listdir(current_dir)
print(f"Файлы в директории: {files}")

# Создание директории
os.makedirs("new_directory", exist_ok=True)

# Проверка существования файла
if os.path.exists("some_file.txt"):
    print("Файл существует")
```

#### Модуль `sys` - взаимодействие с интерпретатором Python

```python
import sys

# Версия Python
print(f"Версия Python: {sys.version}")

# Путь к интерпретатору
print(f"Путь к Python: {sys.executable}")

# Аргументы командной строки
print(f"Аргументы командной строки: {sys.argv}")

# Выход из программы
# sys.exit()  # Завершает программу
```

#### Модуль `math` - математические функции

```python
import math

# Математические функции
print(f"Квадратный корень из 16: {math.sqrt(16)}")
print(f"Синус π/2: {math.sin(math.pi / 2)}")
print(f"Логарифм 100 по основанию 10: {math.log10(100)}")
print(f"Факториал 5: {math.factorial(5)}")

# Округление
print(f"Вверх: {math.ceil(4.2)}")   # 5
print(f"Вниз: {math.floor(4.7)}")   # 4
print(f"Беззнаковое: {math.trunc(-4.7)}")  # -4
```

#### Модуль `random` - генерация случайных чисел

```python
import random

# Случайное целое число
rand_int = random.randint(1, 100)
print(f"Случайное целое от 1 до 100: {rand_int}")

# Случайное число с плавающей точкой
rand_float = random.random()
print(f"Случайное число [0, 1): {rand_float}")

# Случайный выбор из списка
choices = ["яблоко", "банан", "апельсин"]
selected = random.choice(choices)
print(f"Случайный выбор: {selected}")

# Перемешивание списка
numbers = [1, 2, 3, 4, 5]
random.shuffle(numbers)
print(f"Перемешанный список: {numbers}")
```

#### Модуль `datetime` - работа с датой и временем

```python
from datetime import datetime, date, timedelta

# Текущая дата и время
now = datetime.now()
print(f"Сейчас: {now}")

# Только дата
today = date.today()
print(f"Сегодня: {today}")

# Создание конкретной даты
specific_date = date(2023, 12, 25)
print(f"Конкретная дата: {specific_date}")

# Операции с датами
future_date = today + timedelta(days=30)
past_date = today - timedelta(weeks=2)

print(f"Дата через 30 дней: {future_date}")
print(f"Дата 2 недели назад: {past_date}")

# Форматирование даты
formatted_date = now.strftime("%Y-%m-%d %H:%M:%S")
print(f"Отформатированная дата: {formatted_date}")
```

#### Модуль `json` - работа с JSON

```python
import json

# Преобразование Python-объекта в JSON строку
data = {
    "name": "Иван",
    "age": 30,
    "city": "Москва",
    "skills": ["Python", "JavaScript", "SQL"]
}

json_string = json.dumps(data, ensure_ascii=False, indent=2)
print(json_string)

# Преобразование JSON строки в Python-объект
loaded_data = json.loads(json_string)
print(f"Имя: {loaded_data['name']}")
print(f"Навыки: {loaded_data['skills']}")
```

#### Модуль `collections` - расширенные коллекции

```python
from collections import Counter, defaultdict, OrderedDict, deque

# Counter - подсчет количества элементов
text = "программирование"
char_counts = Counter(text)
print(f"Количество букв: {char_counts}")
print(f"Самые частые: {char_counts.most_common(3)}")

# defaultdict - словарь с значением по умолчанию
dd = defaultdict(int)
dd['a'] += 1
dd['b'] += 2
print(dict(dd))  # {'a': 1, 'b': 2}

# deque - двусторонняя очередь
dq = deque([1, 2, 3])
dq.appendleft(0)  # Добавить слева
dq.append(4)      # Добавить справа
print(dq)  # deque([0, 1, 2, 3, 4])
```

### Установка и использование сторонних библиотек

Python Package Index (PyPI) содержит тысячи сторонних библиотек. Установка осуществляется с помощью pip:

```bash
# Установка библиотеки
pip install requests

# Установка конкретной версии
pip install requests==2.28.1

# Установка из requirements.txt
pip install -r requirements.txt
```

Пример использования популярной библиотеки `requests`:

```python
import requests

# GET запрос
response = requests.get("https://httpbin.org/json")
if response.status_code == 200:
    data = response.json()
    print(data)

# POST запрос
payload = {"key1": "value1", "key2": "value2"}
response = requests.post("https://httpbin.org/post", data=payload)
```

### Пакеты (packages)

Пакеты - это способ организации модулей в иерархическую структуру. Пакет - это директория, содержащая файл `__init__.py`:

```
mypackage/
    __init__.py
    module1.py
    module2.py
    subpackage/
        __init__.py
        module3.py
```

```python
# Импорт из пакета
from mypackage import module1
from mypackage.subpackage import module3
import mypackage.module2 as m2
```

Файл `__init__.py` может быть пустым или содержать код инициализации пакета:

```python
# mypackage/__init__.py
"""Мой пакет для работы с геометрией"""

# Определяем, что импортируется при 'from mypackage import *'
__all__ = ['module1', 'module2']

# Код инициализации пакета
print("Пакет mypackage загружен")
```

### Модуль `__main__`

Когда файл запускается как скрипт, специальная переменная `__name__` принимает значение `"__main__"`:

```python
# my_script.py
def main():
    print("Основная функция программы")

def helper_function():
    print("Вспомогательная функция")

# Этот код выполнится только при запуске файла как скрипта
if __name__ == "__main__":
    main()
```

### Виртуальные окружения

Для изоляции зависимостей проектов рекомендуется использовать виртуальные окружения:

```bash
# Создание виртуального окружения
python -m venv myenv

# Активация (Windows)
myenv\Scripts\activate

# Активация (Linux/Mac)
source myenv/bin/activate

# Деактивация
deactivate
```

## Практические примеры

### Пример 1: Создание модуля для работы с датами

Создадим файл `date_utils.py`:

```python
# date_utils.py
from datetime import datetime, timedelta

def days_until(date):
    """Возвращает количество дней до указанной даты"""
    today = datetime.now().date()
    target_date = date.date() if hasattr(date, 'date') else date
    delta = target_date - today
    return delta.days

def format_duration(seconds):
    """Форматирует продолжительность в секундах в удобный формат"""
    hours = seconds // 3600
    minutes = (seconds % 3600) // 60
    secs = seconds % 60
    return f"{hours:02d}:{minutes:02d}:{secs:02d}"

def is_leap_year(year):
    """Проверяет, является ли год високосным"""
    return year % 4 == 0 and (year % 100 != 0 or year % 400 == 0)

def get_weekday_name(date):
    """Возвращает название дня недели"""
    weekdays = ['Понедельник', 'Вторник', 'Среда', 'Четверг', 'Пятница', 'Суббота', 'Воскресенье']
    return weekdays[date.weekday()]
```

Использование модуля:

```python
# main.py
from datetime import date
import date_utils

# Проверка количества дней до Нового Года
new_year = date(2024, 1, 1)
days = date_utils.days_until(new_year)
print(f"До Нового Года осталось {days} дней")

# Проверка високосного года
year = 2024
leap = date_utils.is_leap_year(year)
print(f"{year} год {'високосный' if leap else 'не високосный'}")

# Название дня недели
today = date.today()
weekday = date_utils.get_weekday_name(today)
print(f"Сегодня {weekday}")
```

### Пример 2: Использование модуля `random` для генерации паролей

```python
import random
import string

def generate_password(length=12, include_digits=True, include_symbols=True):
    """Генерирует случайный пароль"""
    chars = string.ascii_letters  # Буквы верхнего и нижнего регистра
    
    if include_digits:
        chars += string.digits
    
    if include_symbols:
        chars += "!@#$%^&*"
    
    password = ''.join(random.choice(chars) for _ in range(length))
    return password

def generate_memorable_password():
    """Генерирует мнемонический пароль"""
    words = ["cat", "dog", "house", "car", "tree", "book", "sun", "moon"]
    numbers = [str(random.randint(10, 99)) for _ in range(2)]
    separator = random.choice(["-", "_", "."])
    
    selected_words = random.sample(words, 2)
    password = separator.join(selected_words + numbers)
    return password

# Примеры использования
simple_password = generate_password()
complex_password = generate_password(16, True, True)
memorable_password = generate_memorable_password()

print(f"Простой пароль: {simple_password}")
print(f"Сложный пароль: {complex_password}")
print(f"Мнемонический пароль: {memorable_password}")
```

### Пример 3: Использование модуля `collections` для анализа текста

```python
from collections import Counter, defaultdict
import re

def analyze_text(text):
    """Анализирует текст и возвращает статистику"""
    # Очистка текста и разделение на слова
    words = re.findall(r'\b\w+\b', text.lower())
    
    # Подсчет частоты слов
    word_freq = Counter(words)
    
    # Группировка слов по длине
    words_by_length = defaultdict(list)
    for word in set(words):
        words_by_length[len(word)].append(word)
    
    return {
        'total_words': len(words),
        'unique_words': len(set(words)),
        'most_common': word_freq.most_common(5),
        'avg_word_length': sum(len(word) for word in words) / len(words) if words else 0,
        'words_by_length': dict(words_by_length)
    }

# Пример использования
sample_text = """
Python - это мощный язык программирования.
Python легко изучать и применять.
Программирование на Python - удовольствие.
"""

stats = analyze_text(sample_text)
print(f"Всего слов: {stats['total_words']}")
print(f"Уникальных слов: {stats['unique_words']}")
print(f"Часто используемые: {stats['most_common']}")
print(f"Средняя длина слова: {stats['avg_word_length']:.2f}")
```

## Заключение

В этой лекции мы подробно рассмотрели модули и библиотеки в Python:

1. **Модули** - файлы с Python-кодом, которые можно импортировать использовать
2. **Способы импорта** - весь модуль, конкретные элементы, с псевдонимами
3. **Стандартная библиотека** - богатый набор модулей, поставляемых с Python
4. **Сторонние библиотеки** - дополнительные пакеты из PyPI
5. **Пакеты** - иерархическая организация модулей
6. **Виртуальные окружения** - изоляция зависимостей проектов

Модули и библиотеки позволяют создавать более организованный, читаемый и поддерживаемый код, а также использовать готовые решения для часто встречающихся задач. В следующей лекции мы рассмотрим обработку исключений в Python.
