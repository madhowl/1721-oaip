# Лекция 12: Работа с файлами

## Введение

Работа с файлами - важная часть программирования, позволяющая сохранять данные между запусками программы, обрабатывать внешние данные и организовывать хранение информации. В этой лекции мы подробно рассмотрим, как работать с файлами в Python: открывать, читать, записывать и закрывать файлы, а также использовать контекстные менеджеры для безопасной работы с файлами.

## Основное содержание

### Открытие файлов

Для работы с файлами в Python используется функция `open()`, которая возвращает объект файла:

```python
# Синтаксис: open(file, mode, encoding)
file_object = open("filename.txt", "r", encoding="utf-8")
```

#### Режимы открытия файлов:

- `'r'` - чтение (по умолчанию)
- `'w'` - запись (перезаписывает файл)
- `'a'` - добавление (записывает в конец файла)
- `'x'` - создание (ошибка, если файл уже существует)
- `'b'` - бинарный режим (например, `'rb'`, `'wb'`)
- `'t'` - текстовый режим (по умолчанию)
- `'+'` - чтение и запись (например, `'r+'`, `'w+'`)

### Чтение файлов

```python
# Открытие и чтение всего файла
file = open("example.txt", "r", encoding="utf-8")
content = file.read()
print(content)
file.close()  # Важно закрыть файл

# Чтение построчно
file = open("example.txt", "r", encoding="utf-8")
for line in file:
    print(line.strip())  # strip() удаляет символы перевода строки
file.close()

# Чтение строк в список
file = open("example.txt", "r", encoding="utf-8")
lines = file.readlines()
print(lines)
file.close()

# Чтение одной строки
file = open("example.txt", "r", encoding="utf-8")
first_line = file.readline()
second_line = file.readline()
print(first_line, second_line)
file.close()
```

### Запись в файлы

```python
# Запись в файл (перезаписывает содержимое)
file = open("output.txt", "w", encoding="utf-8")
file.write("Привет, мир!\n")
file.write("Это вторая строка.\n")
file.close()

# Запись нескольких строк
lines = ["Первая строка\n", "Вторая строка\n", "Третья строка\n"]
file = open("output.txt", "w", encoding="utf-8")
file.writelines(lines)
file.close()
```

### Контекстные менеджеры (with)

Контекстный менеджер `with` автоматически закрывает файл после завершения блока кода:

```python
# Использование with для чтения
with open("example.txt", "r", encoding="utf-8") as file:
    content = file.read()
    print(content)
# Файл автоматически закрывается после выхода из блока with

# Использование with для записи
with open("output.txt", "w", encoding="utf-8") as file:
    file.write("Привет, мир!\n")
    file.write("Это новая строка.\n")
# Файл автоматически закрывается

# Чтение построчно с использованием with
with open("example.txt", "r", encoding="utf-8") as file:
    for line_num, line in enumerate(file, 1):
        print(f"Строка {line_num}: {line.strip()}")
```

### Позиционирование в файле

```python
with open("example.txt", "r", encoding="utf-8") as file:
    # Чтение первых 10 символов
    first_part = file.read(10)
    print(f"Первые 10 символов: {first_part}")
    
    # Получение текущей позиции
    current_pos = file.tell()
    print(f"Текущая позиция: {current_pos}")
    
    # Перемещение в начало файла
    file.seek(0)
    print(f"Позиция после seek(0): {file.tell()}")
    
    # Перемещение на 5 позиций от начала
    file.seek(5)
    remaining = file.read()
    print(f"Остаток файла с 5-й позиции: {remaining}")
```

### Работа с разными типами файлов

#### Текстовые файлы

```python
# Запись и чтение текстового файла
def write_text_file(filename, content):
    with open(filename, 'w', encoding='utf-8') as file:
        file.write(content)

def read_text_file(filename):
    with open(filename, 'r', encoding='utf-8') as file:
        return file.read()

# Пример использования
text_content = "Это пример текстового файла.\nВторая строка.\nТретья строка."
write_text_file("sample.txt", text_content)
read_content = read_text_file("sample.txt")
print(read_content)
```

#### CSV файлы

```python
import csv

# Запись CSV файла
def write_csv_file(filename, data):
    with open(filename, 'w', newline='', encoding='utf-8') as file:
        writer = csv.writer(file)
        writer.writerows(data)

# Чтение CSV файла
def read_csv_file(filename):
    with open(filename, 'r', encoding='utf-8') as file:
        reader = csv.reader(file)
        return list(reader)

# Пример данных
students_data = [
    ["Имя", "Возраст", "Город"],
    ["Иван", "20", "Москва"],
    ["Мария", "22", "СПб"],
    ["Петр", "19", "Новосибирск"]
]

write_csv_file("students.csv", students_data)
csv_data = read_csv_file("students.csv")

for row in csv_data:
    print(row)
```

#### JSON файлы

```python
import json

# Запись JSON файла
def write_json_file(filename, data):
    with open(filename, 'w', encoding='utf-8') as file:
        json.dump(data, file, ensure_ascii=False, indent=2)

# Чтение JSON файла
def read_json_file(filename):
    with open(filename, 'r', encoding='utf-8') as file:
        return json.load(file)

# Пример данных
student_data = {
    "name": "Иван Иванов",
    "age": 20,
    "courses": ["Python", "Math", "English"],
    "grades": {"Python": 5, "Math": 4, "English": 5}
}

write_json_file("student.json", student_data)
loaded_data = read_json_file("student.json")
print(loaded_data)
```

#### Бинарные файлы

```python
# Работа с бинарными файлами
def copy_binary_file(source, destination):
    with open(source, 'rb') as src_file:
        with open(destination, 'wb') as dest_file:
            chunk_size = 1024
            while True:
                chunk = src_file.read(chunk_size)
                if not chunk:
                    break
                dest_file.write(chunk)

# Создание бинарного файла
with open("binary_example.bin", "wb") as file:
    # Запись байтов в файл
    file.write(b"This is binary data\x00\x01\x02")
    file.write((42).to_bytes(4, byteorder='little'))

# Чтение бинарного файла
with open("binary_example.bin", "rb") as file:
    binary_data = file.read()
    print(f"Бинарные данные: {binary_data}")
    print(f"Декодированные байты: {binary_data.decode('ascii', errors='ignore')}")
```

### Обработка исключений при работе с файлами

```python
def safe_read_file(filename):
    try:
        with open(filename, 'r', encoding='utf-8') as file:
            return file.read()
    except FileNotFoundError:
        print(f"Файл {filename} не найден")
        return None
    except PermissionError:
        print(f"Нет доступа к файлу {filename}")
        return None
    except UnicodeDecodeError:
        print(f"Ошибка декодирования файла {filename}")
        return None
    except Exception as e:
        print(f"Произошла ошибка при чтении файла: {e}")
        return None

def safe_write_file(filename, content):
    try:
        with open(filename, 'w', encoding='utf-8') as file:
            file.write(content)
        print(f"Файл {filename} успешно записан")
        return True
    except PermissionError:
        print(f"Нет прав на запись в файл {filename}")
        return False
    except OSError:
        print(f"Ошибка операционной системы при записи в файл {filename}")
        return False
    except Exception as e:
        print(f"Произошла ошибка при записи файла: {e}")
        return False
```

### Работа с директориями

```python
import os
import shutil
from pathlib import Path

# Проверка существования файла или директории
def check_path(path):
    if os.path.exists(path):
        if os.path.isfile(path):
            print(f"{path} - это файл")
        elif os.path.isdir(path):
            print(f"{path} - это директория")
    else:
        print(f"{path} не существует")

# Получение списка файлов в директории
def list_directory(directory):
    try:
        files = os.listdir(directory)
        print(f"Файлы в директории {directory}:")
        for file in files:
            print(f"  {file}")
    except FileNotFoundError:
        print(f"Директория {directory} не найдена")
    except PermissionError:
        print(f"Нет доступа к директории {directory}")

# Создание директории
def create_directory(path):
    try:
        os.makedirs(path, exist_ok=True)
        print(f"Директория {path} создана")
    except Exception as e:
        print(f"Ошибка при создании директории: {e}")

# Удаление файла
def remove_file(filename):
    try:
        os.remove(filename)
        print(f"Файл {filename} удален")
    except FileNotFoundError:
        print(f"Файл {filename} не найден")
    except Exception as e:
        print(f"Ошибка при удалении файла: {e}")

# Примеры использования
check_path("example.txt")
list_directory(".")
create_directory("new_folder")
```

### Продвинутые возможности

#### Использование pathlib

```python
from pathlib import Path

# Создание пути
file_path = Path("data") / "subfolder" / "myfile.txt"

# Проверка существования
if file_path.exists():
    print(f"Файл {file_path} существует")

# Получение информации о файле
print(f"Имя файла: {file_path.name}")
print(f"Родительская директория: {file_path.parent}")
print(f"Расширение: {file_path.suffix}")

# Чтение и запись с использованием pathlib
file_path.write_text("Привет, мир!", encoding="utf-8")
content = file_path.read_text(encoding="utf-8")
print(content)
```

#### Работа с временным файлом

```python
import tempfile

# Создание временного файла
with tempfile.NamedTemporaryFile(mode='w', delete=False, encoding='utf-8') as temp_file:
    temp_file.write("Временные данные")
    temp_filename = temp_file.name
    print(f"Временный файл: {temp_filename}")

# Чтение временного файла
with open(temp_filename, 'r', encoding='utf-8') as file:
    print(f"Содержимое: {file.read()}")

# Удаление временного файла
import os
os.unlink(temp_filename)
```

## Практические примеры

### Пример 1: Логирование в файл

```python
from datetime import datetime
import os

def log_message(log_file, message, level="INFO"):
    timestamp = datetime.now().strftime("%Y-%m-%d %H:%M:%S")
    log_entry = f"[{timestamp}] [{level}] {message}\n"
    
    # Используем режим 'a' для добавления в конец файла
    with open(log_file, 'a', encoding='utf-8') as file:
        file.write(log_entry)

def log_application_event(event_description):
    log_message("app.log", event_description)

# Пример использования
log_application_event("Приложение запущено")
log_application_event("Пользователь вошел в систему", "USER_ACTION")
log_application_event("Ошибка подключения к базе данных", "ERROR")
```

### Пример 2: Работа с конфигурационным файлом

```python
def read_config(config_file):
    """Чтение конфигурационного файла в формате key=value"""
    config = {}
    
    try:
        with open(config_file, 'r', encoding='utf-8') as file:
            for line_num, line in enumerate(file, 1):
                line = line.strip()
                
                # Пропускаем пустые строки и комментарии
                if not line or line.startswith('#'):
                    continue
                
                # Ожидаем формат "ключ=значение"
                if '=' not in line:
                    print(f"Предупреждение: неверный формат в строке {line_num}: {line}")
                    continue
                
                key, value = line.split('=', 1)
                config[key.strip()] = value.strip()
                
    except FileNotFoundError:
        print(f"Конфигурационный файл {config_file} не найден. Используются значения по умолчанию.")
    except Exception as e:
        print(f"Ошибка при чтении конфигурационного файла: {e}")
    
    return config

def write_config(config_file, config_data):
    """Запись конфигурационного файла"""
    try:
        with open(config_file, 'w', encoding='utf-8') as file:
            for key, value in config_data.items():
                file.write(f"{key}={value}\n")
        print(f"Конфигурация сохранена в {config_file}")
    except Exception as e:
        print(f"Ошибка при записи конфигурационного файла: {e}")

# Пример использования
default_config = {
    "database_host": "localhost",
    "database_port": "5432",
    "debug_mode": "True",
    "max_connections": "100"
}

write_config("app_config.txt", default_config)
loaded_config = read_config("app_config.txt")
print("Загруженная конфигурация:", loaded_config)
```

### Пример 3: Обработка большого текстового файла

```python
def process_large_file(input_file, output_file, filter_func=None):
    """Обработка большого файла построчно для экономии памяти"""
    processed_count = 0
    
    with open(input_file, 'r', encoding='utf-8') as infile, \
         open(output_file, 'w', encoding='utf-8') as outfile:
        
        for line in infile:
            # Применяем фильтр, если он предоставлен
            if filter_func is None or filter_func(line):
                outfile.write(line.upper())  # Пример обработки: преобразование в верхний регистр
                processed_count += 1
    
    print(f"Обработано {processed_count} строк")

def line_filter(line):
    """Фильтр: включаем только строки, содержащие определенное слово"""
    return "python" in line.lower()

# Создадим тестовый файл
test_lines = [
    "Python - это отличный язык программирования\n",
    "Java также популярен\n",
    "Я изучаю Python и мне нравится\n",
    "JavaScript используется в веб-разработке\n"
]

with open("input_test.txt", "w", encoding="utf-8") as f:
    f.writelines(test_lines)

# Обработаем файл
process_large_file("input_test.txt", "output_test.txt", line_filter)
```

## Заключение

В этой лекции мы подробно рассмотрели работу с файлами в Python:

1. **Открытие файлов** с различными режимами (чтение, запись, добавление и т.д.)
2. **Чтение и запись** - разными способами (весь файл, построчно, побайтово)
3. **Контекстные менеджеры** (`with`) для безопасной работы с файлами
4. **Работу с разными типами файлов** - текстовыми, CSV, JSON, бинарными
5. **Обработку исключений** при работе с файлами
6. **Продвинутые возможности** с использованием `pathlib` и временных файлов
7. **Практические примеры** применения файловых операций

Работа с файлами является важным аспектом программирования, позволяющим создавать приложения, которые могут сохранять и загружать данные, обрабатывать внешние источники информации и взаимодействовать с файловой системой. В следующей лекции мы рассмотрим основы объектно-ориентированного программирования в Python.
