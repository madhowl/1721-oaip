# Практическая работа 10: Использование модулей

## Цель работы

Научиться использовать встроенные и сторонние модули в Python, импортировать функции и классы из модулей, а также создавать собственные модули для повторного использования кода.

## Теоретическая часть

Модуль - это файл с расширением `.py`, содержащий определения функций, классов и переменных. Модули позволяют организовать код в логические блоки и повторно использовать его в разных программах.

```python
# Пример импорта модуля
import math
import random
from datetime import datetime

# Использование функций из модулей
result = math.sqrt(16)  # 4.0
random_num = random.randint(1, 10)
current_time = datetime.now()
```

## Практические задания

### Задание 1: Использование модуля math

Создайте программу, которая использует различные функции из модуля `math` для выполнения математических операций.

**Пример выполнения:**
```
Введите число для вычисления корня: 25
Квадратный корень из 25: 5.0
Введите радиус круга: 5
Площадь круга: 78.54
```

**Код для выполнения:**
```python
import math

number = float(input("Введите число для вычисления корня: "))
sqrt_result = math.sqrt(number)
print(f"Квадратный корень из {number}: {sqrt_result}")

radius = float(input("Введите радиус круга: "))
area = math.pi * radius ** 2
print(f"Площадь круга: {area:.2f}")

# Дополнительные примеры использования math
angle_degrees = float(input("Введите угол в градусах: "))
angle_radians = math.radians(angle_degrees)
sin_value = math.sin(angle_radians)
cos_value = math.cos(angle_radians)
print(f"Синус {angle_degrees}°: {sin_value:.2f}")
print(f"Косинус {angle_degrees}°: {cos_value:.2f}")
```

---

### Задание 2: Использование модуля random

Создайте программу, которая использует функции из модуля `random` для генерации случайных чисел, выбора случайных элементов и перемешивания списков.

**Пример выполнения:**
```
Случайное число от 1 до 100: 42
Случайный элемент из списка: яблоко
Перемешанный список: ['банан', 'груша', 'яблоко', 'апельсин']
```

**Код для выполнения:**
```python
import random

# Генерация случайного числа
random_int = random.randint(1, 100)
print(f"Случайное число от 1 до 100: {random_int}")

# Случайный выбор из списка
fruits = ["яблоко", "банан", "апельсин", "груша"]
random_fruit = random.choice(fruits)
print(f"Случайный элемент из списка: {random_fruit}")

# Перемешивание списка
print(f"Исходный список: {fruits}")
random.shuffle(fruits)
print(f"Перемешанный список: {fruits}")

# Генерация случайного числа с плавающей точкой
random_float = random.random()
print(f"Случайное число [0, 1): {random_float}")

# Выборка случайных элементов
random_sample = random.sample(range(1, 21), 5)  # 5 случайных чисел от 1 до 20
print(f"Случайная выборка: {random_sample}")
```

---

### Задание 3: Использование модуля datetime

Создайте программу, которая работает с датами и временем, используя модуль `datetime`.

**Пример выполнения:**
```
Текущая дата и время: 2023-10-15 14:30:45
День недели: воскресенье
Оставшееся время до Нового года: 76 дней
```

**Код для выполнения:**
```python
from datetime import datetime, date, timedelta

# Текущая дата и время
now = datetime.now()
print(f"Текущая дата и время: {now.strftime('%Y-%m-%d %H:%M:%S')}")

# День недели
weekdays = ["понедельник", "вторник", "среда", "четверг", "пятница", "суббота", "воскресенье"]
weekday = weekdays[now.weekday()]
print(f"День недели: {weekday}")

# Оставшееся время до Нового года
next_year = now.year + 1
new_year = date(next_year, 1, 1)
current_date = now.date()
days_until_new_year = (new_year - current_date).days
print(f"Оставшееся время до Нового года: {days_until_new_year} дней")

# Разница между двумя датами
birthday = date(2023, 12, 25)
days_until_birthday = (birthday - current_date).days
if days_until_birthday > 0:
    print(f"До дня рождения осталось: {days_until_birthday} дней")
else:
    print("День рождения уже прошел в этом году")
```

---

### Задание 4: Использование модуля os

Создайте программу, которая использует модуль `os` для работы с операционной системой: получение информации о текущей директории, списка файлов, создание директорий.

**Пример выполнения:**
```
Текущая директория: /home/user/documents
Файлы в текущей директории: ['file1.txt', 'file2.py', 'folder1']
```

**Код для выполнения:**
```python
import os

# Текущая директория
current_dir = os.getcwd()
print(f"Текущая директория: {current_dir}")

# Список файлов и папок в текущей директории
files_and_dirs = os.listdir(current_dir)
print(f"Файлы в текущей директории: {files_and_dirs}")

# Создание новой директории
new_dir_name = "test_directory"
if not os.path.exists(new_dir_name):
    os.mkdir(new_dir_name)
    print(f"Директория '{new_dir_name}' создана")
else:
    print(f"Директория '{new_dir_name}' уже существует")

# Проверка существования файла
test_file = "test.txt"
if os.path.exists(test_file):
    print(f"Файл '{test_file}' существует")
    print(f"Размер файла: {os.path.getsize(test_file)} байт")
else:
    print(f"Файл '{test_file}' не существует")

# Обход дерева каталогов
print("\nДерево каталогов (первые 3 уровня):")
for root, dirs, files in os.walk(".", topdown=True):
    level = root.replace(".", "").count(os.sep)
    indent = " " * 2 * level
    print(f"{indent}{os.path.basename(root)}/")
    subindent = " " * 2 * (level + 1)
    for file in files[:5]:  # Показываем только первые 5 файлов
        print(f"{subindent}{file}")
    if level >= 2:  # Ограничиваем глубину
        del dirs[:]
```

---

### Задание 5: Использование модуля sys

Создайте программу, которая использует модуль `sys` для получения информации о системе и аргументах командной строки.

**Пример выполнения:**
```
Версия Python: 3.9.7
Путь к интерпретатору: /usr/bin/python3
Количество аргументов командной строки: 1
```

**Код для выполнения:**
```python
import sys

print(f"Версия Python: {sys.version.split()[0]}")
print(f"Путь к интерпретатору: {sys.executable}")
print(f"Количество аргументов командной строки: {len(sys.argv)}")
print(f"Аргументы командной строки: {sys.argv}")

# Размер объекта в памяти
test_list = [1, 2, 3, 4, 5]
print(f"Размер списка из 5 элементов: {sys.getsizeof(test_list)} байт")

# Размер одного элемента
print(f"Размер одного целого числа: {sys.getsizeof(1)} байт")

# Выход из программы
response = input("Продолжить выполнение программы? (y/n): ")
if response.lower() != 'y':
    print("Завершение программы")
    sys.exit()
```

---

### Задание 6: Использование модуля json

Создайте программу, которая работает с JSON-данными: сериализация и десериализация.

**Пример выполнения:**
```
Оригинальные данные: {'name': 'Иван', 'age': 30, 'city': 'Москва'}
JSON строка: {"name": "Иван", "age": 30, "city": "Москва"}
Загруженные данные: {'name': 'Иван', 'age': 30, 'city': 'Москва'}
```

**Код для выполнения:**
```python
import json

# Создание данных
data = {
    "name": "Иван",
    "age": 30,
    "city": "Москва",
    "hobbies": ["чтение", "плавание", "программирование"]
}

print(f"Оригинальные данные: {data}")

# Сериализация в JSON строку
json_string = json.dumps(data, ensure_ascii=False, indent=2)
print(f"JSON строка: {json_string}")

# Десериализация из JSON строки
loaded_data = json.loads(json_string)
print(f"Загруженные данные: {loaded_data}")

# Работа с файлами JSON
with open("data.json", "w", encoding="utf-8") as file:
    json.dump(data, file, ensure_ascii=False, indent=2)

# Чтение из файла JSON
with open("data.json", "r", encoding="utf-8") as file:
    file_data = json.load(file)
    print(f"Данные из файла: {file_data}")
```

---

### Задание 7: Использование модуля collections

Создайте программу, которая использует модуль `collections` для работы с расширенными структурами данных.

**Пример выполнения:**
```
Счетчик слов: Counter({'python': 3, 'programming': 2, 'language': 1})
Самые частые слова: [('python', 3), ('programming', 2)]
```

**Код для выполнения:**
```python
from collections import Counter, defaultdict, OrderedDict, deque

# Counter - для подсчета элементов
text = "python programming language python is great for programming"
words = text.split()
word_counter = Counter(words)
print(f"Счетчик слов: {word_counter}")
print(f"Самые частые слова: {word_counter.most_common(3)}")

# defaultdict - словарь с значением по умолчанию
dd = defaultdict(int)
for word in words:
    dd[word] += 1
print(f"Словарь с подсчетом: {dict(dd)}")

# OrderedDict - словарь, сохраняющий порядок вставки
ordered_dict = OrderedDict()
ordered_dict["first"] = 1
ordered_dict["second"] = 2
ordered_dict["third"] = 3
print(f"OrderedDict: {ordered_dict}")

# deque - двусторонняя очередь
dq = deque([1, 2, 3])
dq.appendleft(0)  # Добавить слева
dq.append(4)      # Добавить справа
print(f"Deque: {dq}")

# Удаление элементов
left_item = dq.popleft()
right_item = dq.pop()
print(f"Удаленные элементы: {left_item}, {right_item}")
print(f"Оставшийся deque: {dq}")
```

---

### Задание 8: Создание собственного модуля

Создайте собственный модуль с полезными функциями и используйте его в основной программе.

**Пример выполнения:**
```
Созданный модуль utils.py содержит функции для работы с числами и строками
```

**utils.py:**
```python
# utils.py - модуль с полезными функциями

def is_prime(n):
    """Проверяет, является ли число простым"""
    if n < 2:
        return False
    for i in range(2, int(n**0.5) + 1):
        if n % i == 0:
            return False
    return True

def reverse_string(s):
    """Возвращает перевернутую строку"""
    return s[::-1]

def calculate_factorial(n):
    """Вычисляет факториал числа"""
    if n <= 1:
        return 1
    return n * calculate_factorial(n - 1)

def find_max_min(numbers):
    """Находит максимальное и минимальное значение в списке"""
    if not numbers:
        return None, None
    return max(numbers), min(numbers)

def capitalize_words(text):
    """Делает каждое слово в тексте с заглавной буквы"""
    return ' '.join(word.capitalize() for word in text.split())
```

**Основная программа:**
```python
# Импорт собственного модуля
import utils

# Тестирование функций из модуля
print("Проверка числа 17 на простоту:", utils.is_prime(17))
print("Перевернутая строка 'hello':", utils.reverse_string("hello"))
print("Факториал 5:", utils.calculate_factorial(5))

numbers = [3, 1, 4, 1, 5, 9, 2, 6, 5]
max_val, min_val = utils.find_max_min(numbers)
print(f"Максимальное значение: {max_val}, минимальное: {min_val}")

text = "hello world python programming"
capitalized = utils.capitalize_words(text)
print(f"Текст с заглавными буквами: {capitalized}")
```

---

### Задание 9: Использование модуля urllib

Создайте программу, которая использует модуль `urllib` для работы с URL и HTTP-запросами (упрощенная версия, без реальных запросов).

**Пример выполнения:**
```
URL: https://api.example.com/data?param1=value1&param2=value2
Разобранный URL: ParseResult(scheme='https', ...)
```

**Код для выполнения:**
```python
from urllib.parse import urlparse, parse_qs, urlencode
from urllib.request import urlopen

# Работа с URL
url = "https://api.example.com/data?param1=value1&param2=value2&category=tech"
parsed_url = urlparse(url)

print(f"Схема: {parsed_url.scheme}")
print(f"Домен: {parsed_url.netloc}")
