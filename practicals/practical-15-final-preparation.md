# Практическая работа 15: Подготовка к зачёту / итоговая работа

## Цель работы

Обобщить и систематизировать знания, полученные в ходе курса "Основы алгоритмизации и программирования". Выполнить комплексное практическое задание, объединяющее все изученные темы: переменные, типы данных, условные операторы, циклы, функции, структуры данных, обработку исключений и файловый ввод-вывод.

## Теоретическая часть

В рамках курса были изучены следующие ключевые концепции программирования:

1. **Основы алгоритмизации**:
   - Понятие алгоритма
   - Свойства алгоритмов
   - Способы записи алгоритмов

2. **Язык программирования Python**:
   - Синтаксис и структура программы
   - Среды разработки

3. **Типы данных и переменные**:
   - Числовые типы (int, float)
   - Строки (str)
   - Логический тип (bool)
   - Преобразование типов

4. **Условные операторы**:
   - Конструкция if-elif-else
   - Логические операции
   - Вложенные условия

5. **Циклы**:
   - Цикл for
   - Цикл while
   - Вложенные циклы
   - Операторы break и continue

6. **Структуры данных**:
   - Списки (list)
   - Кортежи (tuple)
   - Словари (dict)
   - Множества (set)

7. **Функции**:
   - Определение и вызов функций
   - Параметры и аргументы
   - Возвращаемые значения
   - Область видимости

8. **Модули и библиотеки**:
   - Импорт модулей
   - Стандартная библиотека Python
   - Сторонние библиотеки

9. **Обработка исключений**:
   - Конструкция try-except-finally
   - Виды исключений
   - Генерация исключений

10. **Файловый ввод-вывод**:
    - Открытие и закрытие файлов
    - Чтение и запись
    - Контекстные менеджеры

11. **Основы ООП**:
    - Классы и объекты
    - Атрибуты и методы
    - Наследование, инкапсуляция, полиморфизм

## Практические задания

### Задание 1: Анализ и модификация существующего кода

Проанализируйте следующий код и выполните его модификацию:

```python
# Исходный код (с ошибками)
def calculate_average(numbers):
    total = 0
    for num in numbers:
        total += num
    return total / len(numbers)

def find_max_min(numbers):
    max_val = numbers[0]
    min_val = numbers[0]
    for num in numbers[1:]:
        if num > max_val:
            max_val = num
        if num < min_val:
            min_val = num
    return max_val, min_val

# Использование функций
nums = [1, 2, 3, 4, 5]
avg = calculate_average(nums)
maximum, minimum = find_max_min(nums)

print("Среднее:", avg)
print("Максимум:", maximum)
print("Минимум:", minimum)
```

**Требуется:**
1. Исправить возможные ошибки
2. Добавить обработку исключений
3. Улучшить документирование функций
4. Добавить проверки корректности входных данных

**Код для выполнения:**
```python
def calculate_average(numbers):
    """
    Вычисляет среднее значение списка чисел
    
    Args:
        numbers (list): Список чисел
        
    Returns:
        float: Среднее значение
        
    Raises:
        ValueError: Если список пуст или содержит нечисловые значения
    """
    if not numbers:
        raise ValueError("Список чисел не может быть пустым")
    
    # Проверяем, что все элементы - числа
    for num in numbers:
        if not isinstance(num, (int, float)):
            raise ValueError(f"Найдено нечисловое значение: {num}")
    
    total = sum(numbers)
    return total / len(numbers)

def find_max_min(numbers):
    """
    Находит максимальное и минимальное значение в списке
    
    Args:
        numbers (list): Список чисел
        
    Returns:
        tuple: (максимальное значение, минимальное значение)
        
    Raises:
        ValueError: Если список пуст или содержит нечисловые значения
    """
    if not numbers:
        raise ValueError("Список чисел не может быть пустым")
    
    # Проверяем, что все элементы - числа
    for num in numbers:
        if not isinstance(num, (int, float)):
            raise ValueError(f"Найдено нечисловое значение: {num}")
    
    max_val = min_val = numbers[0]
    for num in numbers[1:]:
        if num > max_val:
            max_val = num
        elif num < min_val:
            min_val = num
    
    return max_val, min_val

# Использование функций с обработкой исключений
nums = [1, 2, 3, 4, 5]

try:
    avg = calculate_average(nums)
    maximum, minimum = find_max_min(nums)
    
    print("Среднее:", avg)
    print("Максимум:", maximum)
    print("Минимум:", minimum)
except ValueError as e:
    print(f"Ошибка: {e}")
```

---

### Задание 2: Создание комплексной программы

Создайте программу "Библиотека", которая включает:
- Систему учета книг (название, автор, год издания, жанр)
- Возможность добавления, удаления, поиска книг
- Систему учета читателей
- Выдачу и возврат книг
- Сохранение данных в файл

**Пример выполнения:**
```
1. Добавить книгу
2. Добавить читателя
3. Выдать книгу
4. Вернуть книгу
5. Поиск книг
6. Показать все книги
7. Показать всех читателей
8. Показать книги у читателей
0. Выход
```

**Код для выполнения:**
```python
import json
from datetime import datetime

class Book:
    """Класс для представления книги"""
    def __init__(self, title, author, year, genre, isbn=None):
        self.title = title
        self.author = author
        self.year = year
        self.genre = genre
        self.isbn = isbn or f"{hash(title + author + str(year)) % 1000000:06d}"
        self.is_available = True
        self.borrowed_by = None
        self.borrowed_date = None

class Reader:
    """Класс для представления читателя"""
    def __init__(self, name, reader_id=None):
        self.name = name
        self.reader_id = reader_id or f"R{hash(name) % 10000:04d}"
        self.borrowed_books = []

class Library:
    """Класс для управления библиотекой"""
    def __init__(self, filename="library_data.json"):
        self.books = {}
        self.readers = {}
        self.filename = filename
        self.load_data()
    
    def add_book(self, title, author, year, genre):
        """Добавляет книгу в библиотеку"""
        book = Book(title, author, year, genre)
        self.books[book.isbn] = book
        print(f"Книга '{title}' добавлена с ISBN: {book.isbn}")
    
    def add_reader(self, name):
        """Добавляет читателя в систему"""
        reader = Reader(name)
        self.readers[reader.reader_id] = reader
        print(f"Читатель '{name}' добавлен с ID: {reader.reader_id}")
    
    def borrow_book(self, isbn, reader_id):
        """Выдает книгу читателю"""
        if isbn not in self.books:
            print("Книга с таким ISBN не найдена")
            return False
        
        if reader_id not in self.readers:
            print("Читатель с таким ID не найден")
            return False
        
        book = self.books[isbn]
        reader = self.readers[reader_id]
        
        if not book.is_available:
            print(f"Книга '{book.title}' уже выдана")
            return False
        
        book.is_available = False
        book.borrowed_by = reader.name
        book.borrowed_date = datetime.now().strftime("%Y-%m-%d")
        reader.borrowed_books.append(isbn)
        
        print(f"Книга '{book.title}' выдана читателю {reader.name}")
        return True
    
    def return_book(self, isbn, reader_id):
        """Принимает возврат книги от читателя"""
        if isbn not in self.books or reader_id not in self.readers:
            print("Книга или читатель не найдены")
            return False
        
        book = self.books[isbn]
        reader = self.readers[reader_id]
        
        if isbn not in reader.borrowed_books:
            print("Эта книга не была выдана данному читателю")
            return False
        
        book.is_available = True
        book.borrowed_by = None
        book.borrowed_date = None
        reader.borrowed_books.remove(isbn)
        
        print(f"Книга '{book.title}' возвращена читателем {reader.name}")
        return True
    
    def search_books(self, query):
        """Поиск книг по названию или автору"""
        results = []
        query = query.lower()
        
        for book in self.books.values():
            if query in book.title.lower() or query in book.author.lower():
                results.append(book)
        
        return results
    
    def display_all_books(self):
        """Показывает все книги"""
        if not self.books:
            print("Нет книг в библиотеке")
            return
        
        print("Все книги в библиотеке:")
        for book in self.books.values():
            status = "доступна" if book.is_available else f"выдана {book.borrowed_by}"
            print(f"ISBN: {book.isbn} | {book.title} ({book.author}, {book.year}) - {status}")
    
    def display_all_readers(self):
        """Показывает всех читателей"""
        if not self.readers:
            print("Нет зарегистрированных читателей")
            return
        
        print("Все зарегистрированные читатели:")
        for reader in self.readers.values():
            borrowed_count = len(reader.borrowed_books)
            print(f"ID: {reader.reader_id} | {reader.name} (взял книг: {borrowed_count})")
    
    def display_borrowed_books(self):
        """Показывает книги, выданные читателям"""
        borrowed_books = [book for book in self.books.values() if not book.is_available]
        
        if not borrowed_books:
            print("Нет выданных книг")
            return
        
        print("Выданные книги:")
        for book in borrowed_books:
            print(f"  '{book.title}' выдана {book.borrowed_by} ({book.borrowed_date})")
    
    def save_data(self):
        """Сохраняет данные в файл"""
        try:
            data = {
                "books": {
                    isbn: {
                        "title": book.title,
                        "author": book.author,
                        "year": book.year,
                        "genre": book.genre,
                        "is_available": book.is_available,
                        "borrowed_by": book.borrowed_by,
                        "borrowed_date": book.borrowed_date
                    } for isbn, book in self.books.items()
                },
                "readers": {
                    reader_id: {
                        "name": reader.name,
                        "borrowed_books": reader.borrowed_books
                    } for reader_id, reader in self.readers.items()
                }
            }
            
            with open(self.filename, 'w', encoding='utf-8') as f:
                json.dump(data, f, ensure_ascii=False, indent=2)
            
            print("Данные сохранены в файл")
        except Exception as e:
            print(f"Ошибка при сохранении данных: {e}")
    
    def load_data(self):
        """Загружает данные из файла"""
        try:
            with open(self.filename, 'r', encoding='utf-8') as f:
                data = json.load(f)
            
            # Восстанавливаем книги
            for isbn, book_data in data.get("books", {}).items():
                book = Book(
                    book_data["title"],
                    book_data["author"],
                    book_data["year"],
                    book_data["genre"],
                    isbn
                )
                book.is_available = book_data["is_available"]
                book.borrowed_by = book_data["borrowed_by"]
                book.borrowed_date = book_data["borrowed_date"]
                self.books[isbn] = book
            
            # Восстанавливаем читателей
            for reader_id, reader_data in data.get("readers", {}).items():
                reader = Reader(reader_data["name"], reader_id)
                reader.borrowed_books = reader_data["borrowed_books"]
                self.readers[reader_id] = reader
            
            print("Данные загружены из файла")
        except FileNotFoundError:
            print("Файл данных не найден, начинаем с пустой библиотеки")
        except Exception as e:
            print(f"Ошибка при загрузке данных: {e}")

# Основная программа
library = Library()

while True:
    print("\n=== Система управления библиотекой ===")
    print("1. Добавить книгу")
    print("2. Добавить читателя")
    print("3. Выдать книгу")
    print("4. Вернуть книгу")
    print("5. Поиск книг")
    print("6. Показать все книги")
    print("7. Показать всех читателей")
    print("8. Показать выданные книги")
    print("9. Сохранить данные")
    print("0. Выход")
    
    choice = input("Выберите действие: ")
    
    if choice == "1":
        title = input("Введите название книги: ")
        author = input("Введите автора: ")
        try:
            year = int(input("Введите год издания: "))
        except ValueError:
            print("Год должен быть числом")
            continue
        genre = input("Введите жанр: ")
        library.add_book(title, author, year, genre)
    
    elif choice == "2":
        name = input("Введите имя читателя: ")
        library.add_reader(name)
    
    elif choice == "3":
        isbn = input("Введите ISBN книги: ")
        reader_id = input("Введите ID читателя: ")
        library.borrow_book(isbn, reader_id)
    
    elif choice == "4":
        isbn = input("Введите ISBN книги: ")
        reader_id = input("Введите ID читателя: ")
        library.return_book(isbn, reader_id)
    
    elif choice == "5":
        query = input("Введите поисковый запрос (название или автор): ")
        results = library.search_books(query)
        if results:
            print("Найденные книги:")
            for book in results:
                status = "доступна" if book.is_available else f"выдана {book.borrowed_by}"
                print(f"  {book.title} ({book.author}, {book.year}) - {status}")
        else:
            print("Книги не найдены")
    
    elif choice == "6":
        library.display_all_books()
    
    elif choice == "7":
        library.display_all_readers()
    
    elif choice == "8":
        library.display_borrowed_books()
    
    elif choice == "9":
        library.save_data()
    
    elif choice == "0":
        library.save_data()  # Сохраняем перед выходом
        print("До свидания!")
        break
    
    else:
        print("Неверный выбор")
```

---

### Задание 3: Решение прикладной задачи

Решите задачу с использованием всех изученных структур данных и концепций программирования:

**Задача**: Создать программу учета доходов и расходов (домашняя бухгалтерия), которая позволяет:
- Вносить транзакции (доходы и расходы) с датой и категорией
- Просматривать историю транзакций
- Фильтровать по дате и категории
- Подсчитывать баланс
- Экспортировать отчеты

**Код для выполнения:**
```python
import json
from datetime import datetime
from collections import defaultdict

class FinanceTracker:
    """Класс для учета финансов"""
    def __init__(self, filename="finance_data.json"):
        self.transactions = []
        self.filename = filename
        self.load_data()
    
    def add_transaction(self, amount, category, trans_type, description="", date=None):
        """Добавляет транзакцию"""
        if trans_type not in ["доход", "расход"]:
            raise ValueError("Тип транзакции должен быть 'доход' или 'расход'")
        
        if date is None:
            date = datetime.now().strftime("%Y-%m-%d")
        
        transaction = {
            "date": date,
            "type": trans_type,
            "amount": float(amount),
            "category": category,
            "description": description
        }
        
        self.transactions.append(transaction)
        print(f"Транзакция добавлена: {trans_type} {amount} руб. ({category})")
    
    def get_balance(self):
        """Возвращает текущий баланс"""
        income = sum(t["amount"] for t in self.transactions if t["type"] == "доход")
        expense = sum(t["amount"] for t in self.transactions if t["type"] == "расход")
        return income - expense
    
    def get_transactions_by_date_range(self, start_date, end_date):
        """Возвращает транзакции в заданном диапазоне дат"""
        start_dt = datetime.strptime(start_date, "%Y-%m-%d")
        end_dt = datetime.strptime(end_date, "%Y-%m-%d")
        
        filtered = []
        for trans in self.transactions:
            trans_dt = datetime.strptime(trans["date"], "%Y-%m-%d")
            if start_dt <= trans_dt <= end_dt:
                filtered.append(trans)
        
        return filtered
    
    def get_expenses_by_category(self):
        """Возвращает расходы по категориям"""
        expenses = defaultdict(float)
        for trans in self.transactions:
            if trans["type"] == "расход":
                expenses[trans["category"]] += trans["amount"]
        return dict(expenses)
    
    def get_income_by_category(self):
        """Возвращает доходы по категориям"""
        income = defaultdict(float)
        for trans in self.transactions:
            if trans["type"] == "доход":
                income[trans["category"]] += trans["amount"]
        return dict(income)
    
    def display_transactions(self, transactions=None):
        """Отображает транзакции"""
        if transactions is None:
            transactions = self.transactions
        
        if not transactions:
            print("Нет транзакций")
            return
        
        print("История транзакций:")
        for i, trans in enumerate(transactions, 1):
            sign = "+" if trans["type"] == "доход" else "-"
            print(f"{i}. {trans['date']} {sign}{trans['amount']:.2f} ({trans['category']}) - {trans['description']}")
    
    def export_report(self, filename):
        """Экспортирует отчет в файл"""
        try:
            report = {
                "balance": self.get_balance(),
                "total_income": sum(t["amount"] for t in self.transactions if t["type"] == "доход"),
                "total_expense": sum(t["amount"] for t in self.transactions if t["type"] == "расход"),
                "transactions": self.transactions,
                "expenses_by_category": self.get_expenses_by_category(),
                "income_by_category": self.get_income_by_category()
            }
            
            with open(filename, 'w', encoding='utf-8') as f:
                json.dump(report, f, ensure_ascii=False, indent=2)
            
            print(f"Отчет экспортирован в {filename}")
        except Exception as e:
            print(f"Ошибка при экспорте отчета: {e}")
    
    def save_data(self):
        """Сохраняет данные в файл"""
        try:
            with open(self.filename, 'w', encoding='utf-8') as f:
                json.dump(self.transactions, f, ensure_ascii=False, indent=2)
            print("Данные сохранены")
        except Exception as e:
            print(f"Ошибка при сохранении: {e}")
    
    def load_data(self):
        """Загружает данные из файла"""
        try:
            with open(self.filename, 'r', encoding='utf-8') as f:
                self.transactions = json.load(f)
            print("Данные загружены")
        except FileNotFoundError:
            print("Файл данных не найден")
        except Exception as e:
            print(f"Ошибка при загрузке: {e}")

# Использование программы
tracker = FinanceTracker()

while True:
    print("\n=== Домашняя бухгалтерия ===")
    print("1. Добавить транзакцию")
    print("2. Показать баланс")
    print("3. Показать транзакции")
    print("4. Фильтр по дате")
    print("5. Расходы по категориям")
    print("6. Доходы по категориям")
    print("7. Экспорт отчета")
    print("0. Выход")
    
    choice = input("Выберите действие: ")
    
    if choice == "1":
        try:
            amount = float(input("Введите сумму: "))
            trans_type = input("Тип (доход/расход): ")
            category = input("Категория: ")
            description = input("Описание (необязательно): ")
            date_input = input("Дата (ГГГГ-ММ-ДД, Enter для сегодня): ")
            
            date = date_input if date_input else None
            tracker.add_transaction(amount, category, trans_type, description, date)
        except ValueError as e:
            print(f"Ошибка: {e}")
    
    elif choice == "2":
        balance = tracker.get_balance()
        print(f"Текущий баланс: {balance:.2f} руб.")
    
    elif choice == "3":
        tracker.display_transactions()
    
    elif choice == "4":
        start_date = input("Начальная дата (ГГГГ-ММ-ДД): ")
        end_date = input("Конечная дата (ГГГГ-ММ-ДД): ")
        filtered = tracker.get_transactions_by_date_range(start_date, end_date)
        tracker.display_transactions(filtered)
    
    elif choice == "5":
        expenses = tracker.get_expenses_by_category()
        print("Расходы по категориям:")
        for category, amount in expenses.items():
            print(f"  {category}: {amount:.2f} руб.")
    
    elif choice == "6":
        income = tracker.get_income_by_category()
        print("Доходы по категориям:")
        for category, amount in income.items():
            print(f"  {category}: {amount:.2f} руб.")
    
    elif choice == "7":
        filename = input("Введите имя файла для экспорта: ")
        tracker.export_report(filename)
    
    elif choice == "0":
        tracker.save_data()
        print("До свидания!")
        break
    
    else:
        print("Неверный выбор")
```

---

### Задание 4: Задача на алгоритмы поиска и сортировки

Реализуйте несколько алгоритмов сортировки и сравните их эффективность:

```python
import time
import random

def bubble_sort(arr):
    """Сортировка пузырьком"""
    n = len(arr)
    comparisons = 0
    swaps = 0
    
    for i in range(n):
        for j in range(0, n-i-1):
            comparisons += 1
            if arr[j] > arr[j+1]:
                arr[j], arr[j+1] = arr[j+1], arr[j]
                swaps += 1
    
    return arr, comparisons, swaps

def selection_sort(arr):
    """Сортировка выбором"""
    n = len(arr)
    comparisons = 0
    swaps = 0
    
    for i in range(n):
        min_idx = i
        for j in range(i+1, n):
            comparisons += 1
            if arr[j] < arr[min_idx]:
                min_idx = j
        
        if min_idx != i:
            arr[i], arr[min_idx] = arr[min_idx], arr[i]
            swaps += 1
    
    return arr, comparisons, swaps

def insertion_sort(arr):
    """Сортировка вставками"""
    comparisons = 0
    swaps = 0
    
    for i in range(1, len(arr)):
        key = arr[i]
        j = i - 1
        
        while j >= 0:
            comparisons += 1
            if arr[j] > key:
                arr[j + 1] = arr[j]
                swaps += 1
                j -= 1
            else:
                break
        
        arr[j + 1] = key
    
    return arr, comparisons, swaps

def quick_sort(arr):
    """Быстрая сортировка"""
    if len(arr) <= 1:
        return arr, 0, 0
    
    comparisons = 0
    swaps = 0
    
    def partition(arr, low, high):
        nonlocal comparisons, swaps
        pivot = arr[high]
        i = low - 1
        
        for j in range(low, high):
            comparisons += 1
            if arr[j] <= pivot:
                i += 1
                arr[i], arr[j] = arr[j], arr[i]
                swaps += 1
        
        arr[i + 1], arr[high] = arr[high], arr[i + 1]
        swaps += 1
        return i + 1
    
    def quick_sort_helper(arr, low, high):
        if low < high:
            pi = partition(arr, low, high)
            quick_sort_helper(arr, low, pi - 1)
            quick_sort_helper(arr, pi + 1, high)
    
    # Создаем копию массива, чтобы не изменять оригинал
    arr_copy = arr.copy()
    quick_sort_helper(arr_copy, 0, len(arr_copy) - 1)
    return arr_copy, comparisons, swaps

# Функция для тестирования алгоритмов
def test_sorting_algorithms():
    sizes = [100, 500, 1000]
    
    for size in sizes:
        print(f"\nТестирование на массиве из {size} элементов:")
        
        # Создаем случайный массив
        original_array = [random.randint(1, 1000) for _ in range(size)]
        
        algorithms = [
            ("Сортировка пузырьком", bubble_sort),
            ("Сортировка выбором", selection_sort),
            ("Сортировка вставками", insertion_sort),
            ("Быстрая сортировка", quick_sort)
        ]
        
        for name, func in algorithms:
            # Создаем копию массива для каждого алгоритма
            test_array = original_array.copy()
            
            start_time = time.time()
            sorted_arr, comparisons, swaps = func(test_array)
            end_time = time.time()
            
            print(f"{name}:")
            print(f"  Время: {end_time - start_time:.6f} сек")
            print(f"  Сравнений: {comparisons}")
            print(f"  Перестановок: {swaps}")

# Запуск тестирования
test_sorting_algorithms()
```

---

## Задание 5: Комплексное задание (итоговое)

Создайте программу "Управление задачами", которая объединяет все изученные концепции:
- Работа с классами
- Использование словарей и списков
- Файловый ввод-вывод
- Обработка исключений
- Функции
- Условные операторы и циклы

Программа должна позволять:
- Создавать задачи с приоритетом и сроком выполнения
- Помечать задачи как выполненные
- Фильтровать задачи по статусу и приоритету
- Сохранять и загружать задачи из файла

**Код для выполнения:**
```python
import json
from datetime import datetime, timedelta

class Task:
    """Класс для представления задачи"""
    def __init__(self, title, description="", priority="средний", due_date=None, task_id=None):
        self.id = task_id or hash(title + str(datetime.now())) % 100000
        self.title = title
        self.description = description
        self.priority = priority  # "низкий", "средний", "высокий"
        self.created_date = datetime.now().strftime("%Y-%m-%d %H:%M:%S")
        self.due_date = due_date
        self.completed = False
        self.completed_date = None
    
    def complete(self):
        """Помечает задачу как выполненную"""
        self.completed = True
        self.completed_date = datetime.now().strftime("%Y-%m-%d %H:%M:%S")
    
    def is_overdue(self):
        """Проверяет, просрочена ли задача"""
        if self.completed or not self.due_date:
            return False
        
        due_dt = datetime.strptime(self.due_date, "%Y-%m-%d")
        return due_dt < datetime.now()
    
    def to_dict(self):
        """Преобразует задачу в словарь для сохранения"""
        return {
            "id": self.id,
            "title": self.title,
            "description": self.description,
            "priority": self.priority,
            "created_date": self.created_date,
            "due_date": self.due_date,
            "completed": self.completed,
            "completed_date": self.completed_date
        }
    
    @classmethod
    def from_dict(cls, data):
        """Создает задачу из словаря"""
        task = cls(
            data["title"],
            data["description"],
            data["priority"],
            data["due_date"],
            data["id"]
        )
        task.completed = data["completed"]
        task.completed_date = data["completed_date"]
        return task

class TaskManager:
    """Класс для управления задачами"""
    def __init__(self, filename="tasks.json"):
        self.tasks = []
        self.filename = filename
        self.load_tasks()
    
    def add_task(self, title, description="", priority="средний", due_date=None):
        """Добавляет новую задачу"""
        try:
            # Проверяем приоритет
            if priority not in ["низкий", "средний", "высокий"]:
                raise ValueError("Приоритет должен быть 'низкий', 'средний' или 'высокий'")
            
            # Проверяем формат даты
            if due_date:
                datetime.strptime(due_date, "%Y-%m-%d")
            
            task = Task(title, description, priority, due_date)
            self.tasks.append(task)
            print(f"Задача '{title}' добавлена с ID: {task.id}")
        except ValueError as e:
            print(f"Ошибка при добавлении задачи: {e}")
    
    def remove_task(self, task_id):
        """Удаляет задачу по ID"""
        for i, task in enumerate(self.tasks):
            if task.id == task_id:
                del self.tasks[i]
                print(f"Задача с ID {task_id} удалена")
                return True
        print(f"Задача с ID {task_id} не найдена")
        return False
    
    def complete_task(self, task_id):
        """Помечает задачу как выполненную"""
        for task in self.tasks:
            if task.id == task_id:
                if not task.completed:
                    task.complete()
                    print(f"Задача '{task.title}' отмечена как выполненная")
                else:
                    print(f"Задача '{task.title}' уже выполнена")
                return True
        print(f"Задача с ID {task_id} не найдена")
        return False
    
    def get_tasks_by_status(self, completed=None):
        """Возвращает задачи по статусу"""
        if completed is None:
            return self.tasks
        return [task for task in self.tasks if task.completed == completed]
    
    def get_tasks_by_priority(self, priority):
        """Возвращает задачи по приоритету"""
        return [task for task in self.tasks if task.priority == priority]
    
    def get_overdue_tasks(self):
        """Возвращает просроченные задачи"""
        return [task for task in self.tasks if task.is_overdue()]
    
    def display_tasks(self, tasks=None):
        """Отображает список задач"""
        if tasks is None:
            tasks = self.tasks
        
        if not tasks:
            print("Нет задач")
            return
        
        print("Список задач:")
        for task in tasks:
            status = "✓" if task.completed else "○"
            overdue = " (ПРОСРОЧЕНА)" if task.is_overdue() and not task.completed else ""
            print(f"{status} [{task.id}] {task.title} (приоритет: {task.priority}){overdue}")
            if task.description:
                print(f"    Описание: {task.description}")
            if task.due_date:
                print(f"    Срок: {task.due_date}")
            print()
    
    def save_tasks(self):
        """Сохраняет задачи в файл"""
        try:
            data = [task.to_dict() for task in self.tasks]
            with open(self.filename, 'w', encoding='utf-8') as f:
                json.dump(data, f, ensure_ascii=False, indent=2)
            print("Задачи сохранены в файл")
        except Exception as e:
            print(f"Ошибка при сохранении задач: {e}")
    
    def load_tasks(self):
        """Загружает задачи из файла"""
        try:
            with open(self.filename, 'r', encoding='utf-8') as f:
                data = json.load(f)
            
            self.tasks = [Task.from_dict(item) for item in data]
            print("Задачи загружены из файла")
        except FileNotFoundError:
            print("Файл задач не найден, начинаем с пустого списка")
        except Exception as e:
            print(f"Ошибка при загрузке задач: {e}")

# Основная программа
tm = TaskManager()

while True:
    print("\n=== Менеджер задач ===")
    print("1. Добавить задачу")
    print("2. Удалить задачу")
    print("3. Отметить задачу выполненной")
    print("4. Показать все задачи")
    print("5. Показать незавершенные задачи")
    print("6. Показать выполненные задачи")
    print("7. Задачи по приоритету")
    print("8. Просроченные задачи")
    print("9. Сохранить задачи")
    print("0. Выход")
    
    try:
        choice = input("Выберите действие: ")
        
        if choice == "1":
            title = input("Название задачи: ")
            description = input("Описание (необязательно): ")
            priority = input("Приоритет (низкий/средний/высокий): ").lower() or "средний"
            due_date = input("Срок выполнения (ГГГГ-ММ-ДД, необязательно): ") or None
            
            tm.add_task(title, description, priority, due_date)
        
        elif choice == "2":
            try:
                task_id = int(input("ID задачи для удаления: "))
                tm.remove_task(task_id)
            except ValueError:
                print("ID должен быть числом")
        
        elif choice == "3":
            try:
                task_id = int(input("ID задачи для завершения: "))
                tm.complete_task(task_id)
            except ValueError:
                print("ID должен быть числом")
        
        elif choice == "4":
            tm.display_tasks()
        
        elif choice == "5":
            incomplete_tasks = tm.get_tasks_by_status(completed=False)
            tm.display_tasks(incomplete_tasks)
        
        elif choice == "6":
            complete_tasks = tm.get_tasks_by_status(completed=True)
            tm.display_tasks(complete_tasks)
        
        elif choice == "7":
            priority = input("Введите приоритет (низкий/средний/высокий): ").lower()
            priority_tasks = tm.get_tasks_by_priority(priority)
            tm.display_tasks(priority_tasks)
        
        elif choice == "8":
            overdue_tasks = tm.get_overdue_tasks()
            if overdue_tasks:
                tm.display_tasks(overdue_tasks)
            else:
                print("Нет просроченных задач")
        
        elif choice == "9":
            tm.save_tasks()
        
        elif choice == "0":
            tm.save_tasks()  # Сохраняем перед выходом
            print("До свидания!")
            break
        
        else:
            print("Неверный выбор")
    except KeyboardInterrupt:
        print("\nПрограмма прервана пользователем")
        tm.save_tasks()
        break
    except Exception as e:
        print(f"Произошла ошибка: {e}")
```

---

## Контрольные вопросы

1. Какие структуры данных вы использовали в этой работе?
2. В чем преимущества использования классов по сравнению с простыми функциями?
3. Как реализована обработка исключений в ваших программах?
4. Какие алгоритмы сортировки вы реализовали?
5. В чем различие между словарями и множествами?
6. Как работает механизм контекстных менеджеров при работе с файлами?
7. Какие приемы использовались для оптимизации кода?
8. Как вы организовали структуру комплексной программы?

## Вывод

В ходе этой практической работы были систематизированы и закреплены все знания, полученные в курсе "Основы алгоритмизации и программирования". Мы:

1. Повторили все основные концепции языка Python
2. Применили знания о структурах данных для решения комплексных задач
3. Использовали объектно-ориентированное программирование для создания сложных приложений
4. Реализовали алгоритмы сортировки и анализа их эффективности
5. Применили файловый ввод-вывод для сохранения данных
6. Использовали обработку исключений для повышения надежности программ

Эта работа завершает цикл практических занятий по основам программирования и готовит к изучению более сложных тем в дальнейшем.
