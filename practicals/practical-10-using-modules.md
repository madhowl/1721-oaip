# Практическая работа 10: Использование модулей

## Цель работы

Научиться использовать встроенные и сторонние модули в Python, освоить импорт модулей, изучить работу с популярными библиотеками, а также создать собственный модуль для повторного использования кода.

## Теоретическая часть

Модуль в Python - это файл с расширением .py, содержащий определения функций, классов и переменных, которые можно импортировать и использовать в других программах. Модули позволяют структурировать код, улучшают читаемость и позволяют повторно использовать функциональность.

```python
# Примеры импорта модулей
import math
import random
from datetime import datetime
from os import path

# Использование функций из модулей
result = math.sqrt(16)  # 4.0
random_num = random.randint(1, 10)
current_time = datetime.now()
```

### Основные способы импорта:
- `import module` - импортирует весь модуль
- `from module import function` - импортирует конкретную функцию
- `from module import *` - импортирует все функции (не рекомендуется)
- `import module as alias` - импортирует с псевдонимом

## Практические задания

### Задание 1: Использование встроенных модулей

Импортируйте модуль `math` и выполните несколько математических операций.

**Пример выполнения:**
```
Квадратный корень из 25: 5.0
Синус угла 90 градусов: 1.0
Факториал 5: 120
Число Пи: 3.141592653589793
```

**Код для выполнения:**
```python
import math

print(f"Квадратный корень из 25: {math.sqrt(25)}")
print(f"Синус угла 90 градусов: {math.sin(math.radians(90))}")
print(f"Факториал 5: {math.factorial(5)}")
print(f"Число Пи: {math.pi}")
print(f"Число e: {math.e}")
print(f"Округление вверх: {math.ceil(4.3)}")
print(f"Округление вниз: {math.floor(4.7)}")
```

---

### Задание 2: Модуль random

Используйте модуль `random` для генерации случайных чисел и выбора элементов.

**Код для выполнения:**
```python
import random

# Случайное число от 1 до 100
random_number = random.randint(1, 100)
print(f"Случайное число: {random_number}")

# Случайное число с плавающей точкой
random_float = random.random()
print(f"Случайное число с плавающей точкой: {random_float}")

# Случайный выбор из списка
colors = ["красный", "зеленый", "синий", "желтый", "оранжевый"]
random_color = random.choice(colors)
print(f"Случайный цвет: {random_color}")

# Перемешивание списка
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
random.shuffle(numbers)
print(f"Перемешанный список: {numbers}")

# Выбор нескольких случайных элементов
random_sample = random.sample(colors, 3)
print(f"Случайная выборка: {random_sample}")
```

---

### Задание 3: Работа с датой и временем

Используйте модуль `datetime` для работы с датами и временем.

**Код для выполнения:**
```python
from datetime import datetime, date, timedelta

# Текущая дата и время
now = datetime.now()
print(f"Сейчас: {now}")

# Текущая дата
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
print(f"Форматированная дата: {formatted_date}")

# Разбор строки с датой
date_string = "2023-10-15"
parsed_date = datetime.strptime(date_string, "%Y-%m-%d")
print(f"Разобранная дата: {parsed_date}")
```

---

### Задание 4: Работа с файловой системой

Используйте модули `os` и `pathlib` для работы с файловой системой.

**Код для выполнения:**
```python
import os
from pathlib import Path

# Текущая директория
current_dir = os.getcwd()
print(f"Текущая директория: {current_dir}")

# Список файлов в директории
files = os.listdir(current_dir)
print(f"Файлы в директории (первые 5): {files[:5]}")

# Создание пути с помощью os.path
file_path = os.path.join(current_dir, "example.txt")
print(f"Путь к файлу: {file_path}")

# Создание пути с помощью pathlib
path_obj = Path(current_dir) / "example.txt"
print(f"Путь с pathlib: {path_obj}")

# Проверка существования файла
if os.path.exists("example.txt"):
    print("Файл example.txt существует")
    print(f"Размер файла: {os.path.getsize('example.txt')} байт")

# Использование pathlib для работы с путями
current_path = Path.cwd()
print(f"Текущая директория (pathlib): {current_path}")

# Поиск файлов с определенным расширением
txt_files = list(current_path.glob("*.txt"))
print(f"TXT файлы: {[f.name for f in txt_files[:5]]}")  # Показываем первые 5
```

---

### Задание 5: Модуль collections

Используйте модуль `collections` для работы с расширенными структурами данных.

**Код для выполнения:**
```python
from collections import Counter, defaultdict, namedtuple, deque

# Counter - подсчет количества элементов
text = "программирование"
char_count = Counter(text)
print(f"Подсчет символов: {char_count}")
print(f"Наиболее частые символы: {char_count.most_common(3)}")

# defaultdict - словарь со значением по умолчанию
dd = defaultdict(int)
dd['a'] += 1
dd['b'] += 2
print(f"Defaultdict: {dict(dd)}")

# namedtuple - именованный кортеж
Point = namedtuple('Point', ['x', 'y'])
p1 = Point(1, 2)
p2 = Point(3, 4)
print(f"Точка p1: x={p1.x}, y={p1.y}")
print(f"Точка p2: x={p2.x}, y={p2.y}")

# deque - двусторонняя очередь
dq = deque([1, 2, 3])
dq.appendleft(0)  # Добавить слева
dq.append(4)      # Добавить справа
print(f"Deque: {dq}")

# Удаление элементов
left = dq.popleft()  # Удалить слева
right = dq.pop()     # Удалить справа
print(f"Удаленные элементы: {left}, {right}")
print(f"Оставшийся deque: {dq}")
```

---

### Задание 6: Модуль itertools

Используйте модуль `itertools` для эффективной работы с итераторами.

**Код для выполнения:**
```python
import itertools

# count() - бесконечный счетчик
counter = itertools.count(start=1, step=2)
print(f"Первые 5 чисел счетчика: {list(itertools.islice(counter, 5))}")

# cycle() - бесконечный цикл по элементам
cycler = itertools.cycle(['A', 'B', 'C'])
print(f"Первые 5 элементов цикла: {list(itertools.islice(cycler, 5))}")

# repeat() - повторение элемента
repeater = itertools.repeat('Hello', 3)
print(f"Повторение: {list(repeater)}")

# combinations() - комбинации
items = ['A', 'B', 'C', 'D']
combos = list(itertools.combinations(items, 2))
print(f"Комбинации по 2: {combos}")

# permutations() - перестановки
perms = list(itertools.permutations(items, 2))
print(f"Перестановки по 2: {perms}")

# product() - декартово произведение
prod = list(itertools.product([1, 2], ['a', 'b']))
print(f"Декартово произведение: {prod}")
```

---

### Задание 7: Модуль functools

Используйте модуль `functools` для работы с функциями.

**Код для выполнения:**
```python
from functools import reduce, lru_cache, partial

# reduce() - применение функции ко всем элементам последовательности
numbers = [1, 2, 3, 4, 5]
sum_result = reduce(lambda x, y: x + y, numbers)
print(f"Сумма: {sum_result}")

# lru_cache - кэширование результатов функции
@lru_cache(maxsize=None)
def fibonacci(n):
    """Вычисляет n-е число Фибоначчи"""
    if n < 2:
        return n
    return fibonacci(n-1) + fibonacci(n-2)

print(f"10-е число Фибоначчи: {fibonacci(10)}")

# partial - создание новой функции с частично примененными аргументами
def multiply(x, y, z):
    return x * y * z

# Создаем функцию, которая всегда умножает на 2
double_multiply = partial(multiply, 2)
result = double_multiply(3, 4)  # эквивалентно multiply(2, 3, 4)
print(f"Результат частичного применения: {result}")
```

---

### Задание 8: Работа с JSON

Используйте модуль `json` для работы с JSON-данными.

**Код для выполнения:**
```python
import json

# Создание данных для JSON
data = {
    "студенты": [
        {"имя": "Иван", "возраст": 20, "оценки": [5, 4, 5, 5]},
        {"имя": "Мария", "возраст": 19, "оценки": [4, 4, 5, 4]},
        {"имя": "Алексей", "возраст": 21, "оценки": [5, 5, 5, 4]}
    ],
    "курс": "Программирование на Python"
}

# Запись в JSON файл
with open("students.json", "w", encoding="utf-8") as jsonfile:
    json.dump(data, jsonfile, ensure_ascii=False, indent=2)

print("Данные записаны в students.json")

# Чтение из JSON файла
with open("students.json", "r", encoding="utf-8") as jsonfile:
    loaded_data = json.load(jsonfile)
    print("Загруженные данные:")
    print(json.dumps(loaded_data, ensure_ascii=False, indent=2))
```

---

### Задание 9: Работа с регулярными выражениями

Используйте модуль `re` для работы с регулярными выражениями.

**Код для выполнения:**
```python
import re

text = "Контактная информация: Иван Иванов - телефон: +7(925)123-45-67, email: ivan@example.com. Мария Петрова - телефон: +7(916)987-65-43, email: maria@test.org."

# Поиск телефонов
phones = re.findall(r'\+7\(\d{3}\)\d{3}-\d{2}-\d{2}', text)
print(f"Найденные телефоны: {phones}")

# Поиск email
emails = re.findall(r'\b[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Z|a-z]{2,}\b', text)
print(f"Найденные email: {emails}")

# Поиск имен
names = re.findall(r'[А-Я][а-я]+\s+[А-Я][а-я]+', text)
print(f"Найденные имена: {names}")

# Замена телефонов на маску
masked_text = re.sub(r'\+7\(\d{3}\)\d{3}-\d{2}-\d{2}', '[ТЕЛЕФОН СКРЫТ]', text)
print(f"Текст с замаскированными телефонами: {masked_text}")

# Разделение текста по нескольким разделителям
text2 = "слово1,слово2;слово3.слово4"
words = re.split(r'[,;.]\s*', text2)
print(f"Разделенные слова: {words}")
```

---

### Задание 10: Создание собственного модуля

Создайте собственный модуль с полезными функциями и импортируйте его.

**Создание модуля my_utils.py:**
```python
# my_utils.py
def calculate_distance(point1, point2):
    """Вычисляет евклидово расстояние между двумя точками"""
    import math
    return math.sqrt((point2[0] - point1[0])**2 + (point2[1] - point1[1])**2)

def is_prime(n):
    """Проверяет, является ли число простым"""
    if n < 2:
        return False
    for i in range(2, int(n**0.5) + 1):
        if n % i == 0:
            return False
    return True

def get_primes(limit):
    """Возвращает список простых чисел до указанного предела"""
    primes = []
    for n in range(2, limit + 1):
        if is_prime(n):
            primes.append(n)
    return primes

def capitalize_words(text):
    """Приводит первую букву каждого слова к заглавной"""
    return ' '.join(word.capitalize() for word in text.split())

def reverse_string(s):
    """Возвращает строку в обратном порядке"""
    return s[::-1]
```

**Использование созданного модуля:**
```python
# Импортируем наш модуль
import my_utils

# Используем функции из модуля
distance = my_utils.calculate_distance((0, 0), (3, 4))
print(f"Расстояние: {distance}")

is_prime_17 = my_utils.is_prime(17)
print(f"17 - простое число: {is_prime_17}")

primes_up_to_20 = my_utils.get_primes(20)
print(f"Простые числа до 20: {primes_up_to_20}")

capitalized = my_utils.capitalize_words("привет мир python")
print(f"С заглавными: {capitalized}")

reversed_str = my_utils.reverse_string("привет")
print(f"Обратная строка: {reversed_str}")
```

---

### Задание 11: Использование сторонних библиотек

Установите и используйте стороннюю библиотеку (на примере requests для HTTP-запросов).

**Код для выполнения:**
```python
# Примечание: перед использованием нужно установить библиотеку:
# pip install requests

try:
    import requests
    
    # Выполнение GET-запроса
    response = requests.get("https://httpbin.org/json")
    
    if response.status_code == 200:
        data = response.json()
        print("Данные получены успешно:")
        print(data)
    else:
        print(f"Ошибка запроса: {response.status_code}")
except ImportError:
    print("Библиотека requests не установлена. Установите с помощью: pip install requests")
except requests.exceptions.RequestException as e:
    print(f"Произошла ошибка при выполнении запроса: {e}")
```

---

### Задание 12: Модуль urllib

Используйте встроенный модуль `urllib` для работы с URL.

**Код для выполнения:**
```python
import urllib.request
import urllib.parse
from urllib.error import URLError, HTTPError

# Пример запроса к веб-ресурсу
try:
    # Открываем URL и читаем содержимое
    with urllib.request.urlopen("https://httpbin.org/json") as response:
        data = response.read().decode('utf-8')
        print("Данные получены с httpbin.org")
        print(data[:200] + "...")  # Показываем первые 200 символов
except HTTPError as e:
    print(f"HTTP ошибка: {e.code} {e.reason}")
except URLError as e:
    print(f"URL ошибка: {e.reason}")

# Кодирование параметров URL
params = {'q': 'Python', 'page': 1}
query_string = urllib.parse.urlencode(params)
print(f"Закодированные параметры: {query_string}")

# Парсинг URL
url = "https://example.com/search?q=python&page=1"
parsed_url = urllib.parse.urlparse(url)
print(f"Схема: {parsed_url.scheme}")
print(f"Домен: {parsed_url.netloc}")
print(f"Путь: {parsed_url.path}")
print(f"Параметры: {parsed_url.query}")
```

---

### Задание 13: Модуль sys

Используйте модуль `sys` для получения информации о системе и аргументах командной строки.

**Код для выполнения:**
```python
import sys

print(f"Версия Python: {sys.version}")
print(f"Путь к интерпретатору: {sys.executable}")
print(f"Аргументы командной строки: {sys.argv}")

# Размер объекта в памяти
my_list = [1, 2, 3, 4, 5]
print(f"Размер списка из 5 элементов: {sys.getsizeof(my_list)} байт")

# Размер одного целого числа
print(f"Размер целого числа: {sys.getsizeof(42)} байт")

# Добавление пути к модулям
# sys.path.append("/путь/к/дополнительным/модулям")

# Выход из программы
# sys.exit("Сообщение об ошибке")
```

---

### Задание 14: Модуль argparse

Используйте модуль `argparse` для создания интерфейса командной строки.

**Код для выполнения:**
```python
import argparse

def main():
    # Создаем парсер аргументов
    parser = argparse.ArgumentParser(description="Пример использования argparse")
    parser.add_argument("name", help="Имя пользователя")
    parser.add_argument("-a", "--age", type=int, default=0, help="Возраст пользователя")
    parser.add_argument("-v", "--verbose", action="store_true", help="Подробный вывод")
    parser.add_argument("--hobby", nargs="+", help="Хобби пользователя")
    
    # Парсим аргументы
    args = parser.parse_args()
    
    # Используем аргументы
    print(f"Привет, {args.name}!")
    if args.age > 0:
        print(f"Вам {args.age} лет")
    
    if args.verbose:
        print("Подробная информация:")
        print(f"  Имя: {args.name}")
        print(f"  Возраст: {args.age}")
        if args.hobby:
            print(f"  Хобби: {', '.join(args.hobby)}")
    
    if args.hobby:
        print(f"Ваши хобби: {', '.join(args.hobby)}")

# Для тестирования в среде разработки создадим тестовую функцию
def test_argparse():
    import sys
    from io import StringIO
    
    # Подменяем sys.argv для тестирования
    original_argv = sys.argv
    sys.argv = ['script.py', 'Иван', '--age', '25', '--hobby', 'программирование', 'теннис']
    
    # Здесь мы не можем полноценно протестировать argparse без реального запуска скрипта
    print("Пример использования argparse:")
    print("python script.py Иван --age 25 --hobby 'программирование' 'теннис' --verbose")
    
    # Восстанавливаем оригинальные аргументы
    sys.argv = original_argv

test_argparse()
```

---

### Задание 15: Модуль statistics

Используйте модуль `statistics` для статистических вычислений.

**Код для выполнения:**
```python
import statistics

data = [1, 2, 3, 4, 5, 5, 6, 7, 8, 9, 10]

print(f"Данные: {data}")
print(f"Среднее: {statistics.mean(data)}")
print(f"Медиана: {statistics.median(data)}")
print(f"Мода: {statistics.mode(data)}")
print(f"Дисперсия: {statistics.variance(data)}")
print(f"Стандартное отклонение: {statistics.stdev(data)}")

# Работа с выборками
sample_data = [2, 4, 4, 4, 5, 5, 7, 9]
print(f"\nВыборочные данные: {sample_data}")
print(f"Среднее выборки: {statistics.mean(sample_data)}")
print(f"Выборочная дисперсия: {statistics.variance(sample_data)}")
print(f"Выборочное стандартное отклонение: {statistics.stdev(sample_data)}")
```

---

## Контрольные вопросы

1. Какие способы импорта модулей вы знаете?
2. В чем разница между `import module` и `from module import function`?
3. Как установить стороннюю библиотеку в Python?
4. Что такое виртуальное окружение и зачем оно нужно?
5. Какие встроенные модули Python вы использовали в работе?
6. Что такое пакет в Python?
7. Как создать собственный модуль?
8. Что такое `__init__.py` файл?
9. Как работает система относительного импорта?
10. Что такое менеджер пакетов pip?

## Вывод

В ходе этой практической работы были изучены различные аспекты работы с модулями в Python:
- Использование встроенных модулей (math, random, datetime, os, collections и др.)
- Работа со сторонними библиотеками
- Создание собственных модулей
- Применение модулей для решения различных задач

Модули позволяют структурировать код, улучшают читаемость и переиспользуемость. Владение навыками работы с модулями является важным элементом профессионального программирования на Python.
