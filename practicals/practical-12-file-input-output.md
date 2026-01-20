# Практическая работа 12: Чтение и запись файлов

## Цель работы

Научиться работать с файлами в Python: открывать, читать, записывать и закрывать файлы, использовать контекстные менеджеры, обрабатывать исключения при работе с файлами, а также применять файловый ввод-вывод для решения задач обработки данных.

## Теоретическая часть

Работа с файлами в Python осуществляется с помощью встроенной функции `open()`, которая возвращает объект файла. Важно правильно открывать и закрывать файлы, использовать контекстные менеджеры для автоматического закрытия файлов, и обрабатывать возможные исключения.

```python
# Базовый синтаксис открытия файла
file = open("filename.txt", "r", encoding="utf-8")
# работа с файлом
file.close()  # обязательно закрыть файл

# Использование контекстного менеджера (рекомендуемый способ)
with open("filename.txt", "r", encoding="utf-8") as file:
    # работа с файлом
    pass  # файл автоматически закроется после выхода из блока with
```

Режимы открытия файлов:
- `'r'` - чтение (по умолчанию)
- `'w'` - запись (существующий файл перезаписывается)
- `'a'` - добавление (запись в конец файла)
- `'x'` - создание (ошибка, если файл существует)
- `'b'` - бинарный режим (например, 'rb', 'wb')
- `'t'` - текстовый режим (по умолчанию)
- `'+'` - чтение и запись (например, 'r+', 'w+')

## Практические задания

### Задание 1: Создание и запись в файл

Создайте программу, которая создает текстовый файл и записывает в него несколько строк текста.

**Пример выполнения:**
```
Создан файл example.txt с содержимым:
Строка 1
Строка 2
Строка 3
```

**Код для выполнения:**
```python
# Запись в файл
with open("example.txt", "w", encoding="utf-8") as file:
    file.write("Строка 1\n")
    file.write("Строка 2\n")
    file.write("Строка 3\n")

print("Файл example.txt создан с содержимым:")
with open("example.txt", "r", encoding="utf-8") as file:
    content = file.read()
    print(content)
```

---

### Задание 2: Чтение файла построчно

Создайте программу, которая читает файл построчно и выводит каждую строку с номером.

**Пример выполнения:**
```
1: Строка 1
2: Строка 2
3: Строка 3
```

**Код для выполнения:**
```python
with open("example.txt", "r", encoding="utf-8") as file:
    for line_num, line in enumerate(file, 1):
        print(f"{line_num}: {line.strip()}")
```

---

### Задание 3: Работа с методами чтения

Используйте разные методы чтения файла: `read()`, `readline()`, `readlines()`.

**Код для выполнения:**
```python
# Создадим тестовый файл
with open("test.txt", "w", encoding="utf-8") as f:
    f.write("Первая строка\nВторая строка\nТретья строка\nЧетвертая строка")

# Пример использования различных методов чтения
print("=== Чтение всего файла с read() ===")
with open("test.txt", "r", encoding="utf-8") as f:
    content = f.read()
    print(content)

print("\n=== Чтение по одной строке с readline() ===")
with open("test.txt", "r", encoding="utf-8") as f:
    line1 = f.readline()
    line2 = f.readline()
    print(f"Первая строка: {line1.strip()}")
    print(f"Вторая строка: {line2.strip()}")

print("\n=== Чтение всех строк с readlines() ===")
with open("test.txt", "r", encoding="utf-8") as f:
    lines = f.readlines()
    for i, line in enumerate(lines, 1):
        print(f"Строка {i}: {line.strip()}")
```

---

### Задание 4: Добавление данных в файл

Создайте программу, которая добавляет новые строки в существующий файл.

**Пример выполнения:**
```
Введите текст для добавления: Новая строка
Текст добавлен в файл
```

**Код для выполнения:**
```python
new_text = input("Введите текст для добавления: ")

with open("example.txt", "a", encoding="utf-8") as file:
    file.write(new_text + "\n")

print("Текст добавлен в файл")
```

---

### Задание 5: Копирование файла

Создайте программу, которая копирует содержимое одного файла в другой.

**Код для выполнения:**
```python
def copy_file(source, destination):
    """Копирует содержимое файла source в файл destination"""
    try:
        with open(source, "r", encoding="utf-8") as src:
            with open(destination, "w", encoding="utf-8") as dst:
                content = src.read()
                dst.write(content)
        print(f"Файл {source} скопирован в {destination}")
    except FileNotFoundError:
        print(f"Файл {source} не найден")
    except Exception as e:
        print(f"Произошла ошибка: {e}")

# Пример использования
copy_file("example.txt", "copy_example.txt")
```

---

### Задание 6: Подсчет слов в файле

Создайте программу, которая подсчитывает количество слов в текстовом файле.

**Код для выполнения:**
```python
def count_words_in_file(filename):
    """Подсчитывает количество слов в файле"""
    try:
        with open(filename, "r", encoding="utf-8") as file:
            content = file.read()
            words = content.split()
            return len(words)
    except FileNotFoundError:
        print(f"Файл {filename} не найден")
        return 0
    except Exception as e:
        print(f"Произошла ошибка: {e}")
        return 0

filename = input("Введите имя файла: ")
word_count = count_words_in_file(filename)
print(f"Количество слов в файле: {word_count}")
```

---

### Задание 7: Работа с CSV файлами

Создайте программу, которая создает и читает CSV файл (файл с разделенными запятыми значениями).

**Пример выполнения:**
```
Создан файл data.csv
Имя,Возраст,Город
Иван,25,Москва
Мария,30,СПб
```

**Код для выполнения:**
```python
import csv

# Создание CSV файла
data = [
    ["Имя", "Возраст", "Город"],
    ["Иван", "25", "Москва"],
    ["Мария", "30", "СПб"],
    ["Алексей", "22", "Новосибирск"]
]

with open("data.csv", "w", newline='', encoding="utf-8") as csvfile:
    writer = csv.writer(csvfile)
    writer.writerows(data)

print("Создан файл data.csv")

# Чтение CSV файла
print("Содержимое файла:")
with open("data.csv", "r", encoding="utf-8") as csvfile:
    reader = csv.reader(csvfile)
    for row in reader:
        print(",".join(row))
```

---

### Задание 8: Работа с JSON файлами

Создайте программу, которая записывает и читает данные в формате JSON.

**Код для выполнения:**
```python
import json

# Данные для записи
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

### Задание 9: Поиск в файле

Создайте программу, которая ищет определенное слово в текстовом файле и выводит строки, содержащие это слово.

**Код для выполнения:**
```python
def search_in_file(filename, search_term):
    """Ищет строку в файле и выводит строки с совпадениями"""
    try:
        with open(filename, "r", encoding="utf-8") as file:
            for line_num, line in enumerate(file, 1):
                if search_term.lower() in line.lower():
                    print(f"Строка {line_num}: {line.strip()}")
    except FileNotFoundError:
        print(f"Файл {filename} не найден")
    except Exception as e:
        print(f"Произошла ошибка: {e}")

filename = input("Введите имя файла для поиска: ")
search_term = input("Введите слово для поиска: ")
search_in_file(filename, search_term)
```

---

### Задание 10: Обработка лог-файла

Создайте программу, которая анализирует лог-файл и подсчитывает количество событий по типам.

**Пример лог-файла (log.txt):**
```
2023-10-01 10:00:00 INFO: Приложение запущено
2023-10-01 10:05:23 ERROR: Ошибка подключения к базе данных
2023-10-01 10:06:45 WARNING: Мало свободной памяти
2023-10-01 10:07:12 INFO: Пользователь вошел в систему
2023-10-01 10:08:30 ERROR: Ошибка аутентификации
```

**Код для выполнения:**
```python
def analyze_log_file(filename):
    """Анализирует лог-файл и подсчитывает количество событий по типам"""
    counts = {"INFO": 0, "WARNING": 0, "ERROR": 0, "DEBUG": 0}
    
    try:
        with open(filename, "r", encoding="utf-8") as file:
            for line in file:
                if "INFO" in line:
                    counts["INFO"] += 1
                elif "WARNING" in line:
                    counts["WARNING"] += 1
                elif "ERROR" in line:
                    counts["ERROR"] += 1
                elif "DEBUG" in line:
                    counts["DEBUG"] += 1
    except FileNotFoundError:
        print(f"Файл {filename} не найден")
        return counts
    except Exception as e:
        print(f"Произошла ошибка: {e}")
        return counts
    
    return counts

# Создадим тестовый лог-файл
log_content = """2023-10-01 10:00:00 INFO: Приложение запущено
2023-10-01 10:05:23 ERROR: Ошибка подключения к базе данных
2023-10-01 10:06:45 WARNING: Мало свободной памяти
2023-10-01 10:07:12 INFO: Пользователь вошел в систему
2023-10-01 10:08:30 ERROR: Ошибка аутентификации
2023-10-01 10:09:15 DEBUG: Отладочное сообщение"""

with open("log.txt", "w", encoding="utf-8") as f:
    f.write(log_content)

# Анализ лог-файла
results = analyze_log_file("log.txt")
print("Результаты анализа лог-файла:")
for level, count in results.items():
    print(f"{level}: {count}")
```

---

### Задание 11: Резервное копирование файлов

Создайте программу, которая создает резервную копию файла с добавлением даты к имени файла.

**Код для выполнения:**
```python
import shutil
import datetime

def backup_file(source_file):
    """Создает резервную копию файла с добавлением даты"""
    # Получаем текущую дату и время
    now = datetime.datetime.now()
    timestamp = now.strftime("%Y%m%d_%H%M%S")
    
    # Формируем имя резервного файла
    parts = source_file.split('.')
    if len(parts) > 1:
        backup_name = '.'.join(parts[:-1]) + f"_backup_{timestamp}.{parts[-1]}"
    else:
        backup_name = f"{source_file}_backup_{timestamp}"
    
    try:
        shutil.copy2(source_file, backup_name)
        print(f"Резервная копия создана: {backup_name}")
        return backup_name
    except FileNotFoundError:
        print(f"Файл {source_file} не найден")
        return None
    except Exception as e:
        print(f"Произошла ошибка при создании резервной копии: {e}")
        return None

# Пример использования
backup_file("example.txt")
```

---

### Задание 12: Обработка бинарных файлов

Создайте программу, которая читает и записывает бинарные файлы.

**Код для выполнения:**
```python
# Запись бинарного файла
data = bytes([65, 66, 67, 68, 69])  # байты для 'ABCDE'
with open("binary_example.bin", "wb") as f:
    f.write(data)

print("Бинарный файл записан")

# Чтение бинарного файла
with open("binary_example.bin", "rb") as f:
    binary_data = f.read()
    print(f"Бинарные данные: {binary_data}")
    print(f"Декодированные символы: {binary_data.decode('ascii', errors='ignore')}")

# Копирование бинарного файла
with open("binary_example.bin", "rb") as src:
    with open("binary_copy.bin", "wb") as dst:
        chunk_size = 1024
        while True:
            chunk = src.read(chunk_size)
            if not chunk:
                break
            dst.write(chunk)

print("Бинарный файл скопирован")
```

---

### Задание 13: Работа с путями к файлам

Используйте модуль `os` или `pathlib` для работы с путями к файлам.

**Код для выполнения:**
```python
import os
from pathlib import Path

# Использование os
print("=== Работа с os ===")
current_dir = os.getcwd()
print(f"Текущая директория: {current_dir}")

files = os.listdir(current_dir)
print(f"Файлы в директории: {files[:5]}...")  # Показываем первые 5

# Проверка существования файла
if os.path.exists("example.txt"):
    print("Файл example.txt существует")
    print(f"Размер файла: {os.path.getsize('example.txt')} байт")

# Использование pathlib
print("\n=== Работа с pathlib ===")
current_path = Path.cwd()
print(f"Текущая директория: {current_path}")

# Поиск файлов с определенным расширением
txt_files = list(current_path.glob("*.txt"))
print(f"TXT файлы: {[f.name for f in txt_files]}")

# Создание нового пути
new_file = current_path / "new_directory" / "new_file.txt"
print(f"Новый путь: {new_file}")
print(f"Родительская директория: {new_file.parent}")
print(f"Имя файла: {new_file.name}")
print(f"Расширение: {new_file.suffix}")
```

---

### Задание 14: Безопасная запись в файл

Создайте функцию, которая безопасно записывает данные в файл, создавая резервную копию старого файла.

**Код для выполнения:**
```python
import shutil
import os

def safe_write_to_file(filename, content):
    """Безопасно записывает содержимое в файл, создавая резервную копию"""
    # Если файл существует, создаем резервную копию
    if os.path.exists(filename):
        backup_name = filename + ".bak"
        shutil.copy2(filename, backup_name)
        print(f"Создана резервная копия: {backup_name}")
    
    # Записываем новое содержимое
    try:
        with open(filename, "w", encoding="utf-8") as f:
            f.write(content)
        print(f"Данные записаны в файл {filename}")
        return True
    except Exception as e:
        print(f"Ошибка при записи в файл: {e}")
        # Восстанавливаем из резервной копии, если она была
        if os.path.exists(filename + ".bak"):
            shutil.move(filename + ".bak", filename)
            print("Файл восстановлен из резервной копии")
        return False

# Пример использования
success = safe_write_to_file("safe_example.txt", "Это безопасная запись\nВторая строка")
if success:
    print("Запись прошла успешно")
```

---

### Задание 15: Комплексная задача - журнал учета задач

Создайте простую систему учета задач, которая сохраняет и загружает задачи из файла.

**Код для выполнения:**
```python
import json
import os
from datetime import datetime

class TaskManager:
    def __init__(self, filename="tasks.json"):
        self.filename = filename
        self.tasks = self.load_tasks()
    
    def load_tasks(self):
        """Загружает задачи из файла"""
        if os.path.exists(self.filename):
            try:
                with open(self.filename, "r", encoding="utf-8") as f:
                    return json.load(f)
            except Exception as e:
                print(f"Ошибка при загрузке задач: {e}")
                return []
        return []
    
    def save_tasks(self):
        """Сохраняет задачи в файл"""
        try:
            with open(self.filename, "w", encoding="utf-8") as f:
                json.dump(self.tasks, f, ensure_ascii=False, indent=2)
            return True
        except Exception as e:
            print(f"Ошибка при сохранении задач: {e}")
            return False
    
    def add_task(self, title, description=""):
        """Добавляет новую задачу"""
        task = {
            "id": len(self.tasks) + 1,
            "title": title,
            "description": description,
            "completed": False,
            "created_at": datetime.now().isoformat()
        }
        self.tasks.append(task)
        return self.save_tasks()
    
    def list_tasks(self):
        """Выводит список всех задач"""
        if not self.tasks:
            print("Нет задач")
            return
        
        for task in self.tasks:
            status = "✓" if task["completed"] else "○"
            print(f"{status} [{task['id']}] {task['title']}")
            if task["description"]:
                print(f"    {task['description']}")
    
    def complete_task(self, task_id):
        """Отмечает задачу как выполненную"""
        for task in self.tasks:
            if task["id"] == task_id:
                task["completed"] = True
                return self.save_tasks()
        return False
    
    def delete_task(self, task_id):
        """Удаляет задачу"""
        self.tasks = [task for task in self.tasks if task["id"] != task_id]
        return self.save_tasks()

# Пример использования
tm = TaskManager()

while True:
    print("\n1. Добавить задачу")
    print("2. Показать задачи")
    print("3. Отметить задачу выполненной")
    print("4. Удалить задачу")
    print("5. Выйти")
    
    choice = input("Выберите действие: ")
    
    if choice == "1":
        title = input("Введите название задачи: ")
        description = input("Введите описание задачи (необязательно): ")
        if tm.add_task(title, description):
            print("Задача добавлена")
        else:
            print("Ошибка при добавлении задачи")
    elif choice == "2":
        print("\nСписок задач:")
        tm.list_tasks()
    elif choice == "3":
        task_id = int(input("Введите ID задачи для отметки: "))
        if tm.complete_task(task_id):
            print("Задача отмечена как выполненная")
        else:
            print("Задача не найдена")
    elif choice == "4":
        task_id = int(input("Введите ID задачи для удаления: "))
        if tm.delete_task(task_id):
            print("Задача удалена")
        else:
            print("Задача не найдена")
    elif choice == "5":
        break
    else:
        print("Неверный выбор")
```

---

## Контрольные вопросы

1. Как открыть файл для чтения в Python?
2. В чем разница между режимами 'w' и 'a' при открытии файла?
3. Что такое контекстный менеджер и зачем он используется?
4. Какие методы существуют для чтения данных из файла?
5. Как обработать исключение при открытии несуществующего файла?
6. Что такое бинарный режим работы с файлами?
7. Как записать данные в формате JSON в файл?
8. Какие существуют способы обработки CSV файлов?
9. Как получить список файлов в директории?
10. В чем преимущества использования pathlib по сравнению с os.path?

## Вывод

В ходе этой практической работы были освоены основы работы с файлами в Python. Были рассмотрены различные режимы открытия файлов, методы чтения и записи данных, использование контекстных менеджеров для безопасной работы с файлами, а также применение файлового ввода-вывода для решения различных задач. Правильная работа с файлами является важным навыком при разработке программ, которые должны сохранять и загружать данные.
