# Лекция 16: Решение прикладных задач

## Введение

После изучения всех основных концепций программирования на Python - от базовых типов данных до алгоритмов поиска и сортировки - настало время применить полученные знания к решению реальных прикладных задач. В этой лекции мы рассмотрим комплексные задачи, которые объединяют несколько концепций и требуют применения различных структур данных и алгоритмов для их решения.

## Основное содержание

### Задача 1: Система управления библиотекой

Разработаем систему управления библиотекой, которая будет использовать различные структуры данных и алгоритмы для эффективной работы с книгами и читателями.

```python
from datetime import datetime, timedelta
from typing import List, Dict, Optional

class Book:
    """Класс, представляющий книгу"""
    def __init__(self, isbn: str, title: str, author: str, year: int):
        self.isbn = isbn
        self.title = title
        self.author = author
        self.year = year
        self.is_available = True
        self.borrowed_by = None
        self.borrowed_date = None
        self.due_date = None
    
    def __str__(self):
        status = "доступна" if self.is_available else f"взята {self.borrowed_by}"
        return f"{self.title} ({self.author}, {self.year}) - {status}"

class Reader:
    """Класс, представляющий читателя"""
    def __init__(self, reader_id: str, name: str, email: str):
        self.reader_id = reader_id
        self.name = name
        self.email = email
        self.borrowed_books = []
        self.borrow_history = []
    
    def __str__(self):
        return f"{self.name} ({self.email})"

class LibrarySystem:
    """Система управления библиотекой"""
    def __init__(self):
        self.books: Dict[str, Book] = {}  # Словарь книг (ключ - ISBN)
        self.readers: Dict[str, Reader] = {}  # Словарь читателей (ключ - ID)
        self.book_title_index: Dict[str, List[str]] = {}  # Индекс по названиям книг
        self.book_author_index: Dict[str, List[str]] = {}  # Индекс по авторам
    
    def add_book(self, book: Book):
        """Добавить книгу в библиотеку"""
        self.books[book.isbn] = book
        
        # Обновляем индексы для быстрого поиска
        self._update_title_index(book)
        self._update_author_index(book)
    
    def _update_title_index(self, book: Book):
        """Обновить индекс по названию книги"""
        title_lower = book.title.lower()
        if title_lower not in self.book_title_index:
            self.book_title_index[title_lower] = []
        self.book_title_index[title_lower].append(book.isbn)
    
    def _update_author_index(self, book: Book):
        """Обновить индекс по автору книги"""
        author_lower = book.author.lower()
        if author_lower not in self.book_author_index:
            self.book_author_index[author_lower] = []
        self.book_author_index[author_lower].append(book.isbn)
    
    def register_reader(self, reader: Reader):
        """Зарегистрировать читателя"""
        self.readers[reader.reader_id] = reader
    
    def search_by_title(self, title: str) -> List[Book]:
        """Поиск книг по названию (с частичным совпадением)"""
        title_lower = title.lower()
        results = []
        
        # Линейный поиск по индексу названий
        for indexed_title, isbn_list in self.book_title_index.items():
            if title_lower in indexed_title:
                for isbn in isbn_list:
                    results.append(self.books[isbn])
        
        return results
    
    def search_by_author(self, author: str) -> List[Book]:
        """Поиск книг по автору (с частичным совпадением)"""
        author_lower = author.lower()
        results = []
        
        # Линейный поиск по индексу авторов
        for indexed_author, isbn_list in self.book_author_index.items():
            if author_lower in indexed_author:
                for isbn in isbn_list:
                    results.append(self.books[isbn])
        
        return results
    
    def borrow_book(self, isbn: str, reader_id: str) -> bool:
        """Выдать книгу читателю"""
        if isbn not in self.books:
            print(f"Книга с ISBN {isbn} не найдена")
            return False
        
        if reader_id not in self.readers:
            print(f"Читатель с ID {reader_id} не зарегистрирован")
            return False
        
        book = self.books[isbn]
        reader = self.readers[reader_id]
        
        if not book.is_available:
            print(f"Книга '{book.title}' уже взята")
            return False
        
        # Выдаем книгу
        book.is_available = False
        book.borrowed_by = reader.name
        book.borrowed_date = datetime.now()
        book.due_date = datetime.now() + timedelta(days=30)  # Срок возврата - 30 дней
        
        reader.borrowed_books.append(isbn)
        reader.borrow_history.append({
            'isbn': isbn,
            'title': book.title,
            'borrow_date': book.borrowed_date,
            'due_date': book.due_date
        })
        
        print(f"Книга '{book.title}' выдана читателю {reader.name}")
        return True
    
    def return_book(self, isbn: str, reader_id: str) -> bool:
        """Вернуть книгу в библиотеку"""
        if isbn not in self.books:
            print(f"Книга с ISBN {isbn} не найдена")
            return False
        
        book = self.books[isbn]
        reader = self.readers.get(reader_id)
        
        if reader is None or isbn not in reader.borrowed_books:
            print(f"Книга не была выдана этому читателю")
            return False
        
        # Возвращаем книгу
        book.is_available = True
        book.borrowed_by = None
        book.borrowed_date = None
        book.due_date = None
        
        reader.borrowed_books.remove(isbn)
        
        print(f"Книга '{book.title}' возвращена читателем {reader.name}")
        return True
    
    def get_overdue_books(self) -> List[Dict]:
        """Получить список просроченных книг"""
        overdue_books = []
        current_date = datetime.now()
        
        for book in self.books.values():
            if not book.is_available and book.due_date < current_date:
                overdue_books.append({
                    'book': book,
                    'days_overdue': (current_date - book.due_date).days
                })
        
        return overdue_books
    
    def get_reader_books(self, reader_id: str) -> List[Book]:
        """Получить список книг, взятых читателем"""
        reader = self.readers.get(reader_id)
        if reader is None:
            return []
        
        return [self.books[isbn] for isbn in reader.borrowed_books]

# Пример использования системы
def library_system_demo():
    # Создаем систему
    library = LibrarySystem()
    
    # Добавляем книги
    books_data = [
        ("978-0-123456-78-9", "Война и мир", "Лев Толстой", 1869),
        ("978-0-987654-32-1", "Преступление и наказание", "Федор Достоевский", 1866),
        ("978-0-456789-12-3", "1984", "Джордж Оруэлл", 1949),
        ("978-0-321654-98-7", "Мастер и Маргарита", "Михаил Булгаков", 1967),
        ("978-0-789456-12-5", "Анна Каренина", "Лев Толстой", 1877)
    ]
    
    for isbn, title, author, year in books_data:
        book = Book(isbn, title, author, year)
        library.add_book(book)
    
    # Регистрируем читателей
    readers_data = [
        ("R001", "Иван Иванов", "ivan@example.com"),
        ("R002", "Мария Петрова", "maria@example.com"),
        ("R003", "Алексей Сидоров", "alexey@example.com")
    ]
    
    for reader_id, name, email in readers_data:
        reader = Reader(reader_id, name, email)
        library.register_reader(reader)
    
    # Демонстрируем функциональность
    print("=== Поиск книг ===")
    tolstoy_books = library.search_by_author("толстой")
    print(f"Книги Льва Толстого: {len(tolstoy_books)}")
    for book in tolstoy_books:
        print(f"  - {book}")
    
    print("\n=== Выдача книг ===")
    library.borrow_book("978-0-123456-78-9", "R001")  # Война и мир Ивану
    library.borrow_book("978-0-456789-12-3", "R001")  # 1984 Ивану
    library.borrow_book("978-0-987654-32-1", "R002")  # Преступление и наказание Марии
    
    print("\n=== Книги, взятые Иваном ===")
    ivan_books = library.get_reader_books("R001")
    for book in ivan_books:
        print(f"  - {book}")
    
    print("\n=== Возврат книги ===")
    library.return_book("978-0-123456-78-9", "R001")  # Война и мир возвращается
    
    print("\n=== Проверка просроченных книг ===")
    overdue = library.get_overdue_books()
    if overdue:
        for item in overdue:
            print(f"  - {item['book'].title} просрочена на {item['days_overdue']} дней")
    else:
        print("  Нет просроченных книг")

library_system_demo()
```

### Задача 2: Анализ данных о продажах

Разработаем систему анализа данных о продажах, которая будет использовать различные алгоритмы обработки и анализа данных.

```python
from typing import List, Dict, Tuple
from collections import defaultdict
import statistics

class SaleRecord:
    """Класс, представляющий запись о продаже"""
    def __init__(self, sale_id: str, product: str, category: str, price: float, quantity: int, date: str, region: str):
        self.sale_id = sale_id
        self.product = product
        self.category = category
        self.price = price
        self.quantity = quantity
        self.date = date
        self.region = region
        self.total_amount = price * quantity

class SalesAnalyzer:
    """Анализатор данных о продажах"""
    def __init__(self):
        self.sales_records: List[SaleRecord] = []
        self.category_totals: Dict[str, float] = defaultdict(float)
        self.product_sales: Dict[str, int] = defaultdict(int)
        self.region_sales: Dict[str, float] = defaultdict(float)
    
    def add_sale(self, record: SaleRecord):
        """Добавить запись о продаже"""
        self.sales_records.append(record)
        
        # Обновляем статистику
        self.category_totals[record.category] += record.total_amount
        self.product_sales[record.product] += record.quantity
        self.region_sales[record.region] += record.total_amount
    
    def get_total_revenue(self) -> float:
        """Получить общую выручку"""
        return sum(record.total_amount for record in self.sales_records)
    
    def get_top_categories(self, n: int = 5) -> List[Tuple[str, float]]:
        """Получить топ N категорий по выручке"""
        sorted_categories = sorted(self.category_totals.items(), key=lambda x: x[1], reverse=True)
        return sorted_categories[:n]
    
    def get_top_products(self, n: int = 10) -> List[Tuple[str, int]]:
        """Получить топ N товаров по количеству продаж"""
        sorted_products = sorted(self.product_sales.items(), key=lambda x: x[1], reverse=True)
        return sorted_products[:n]
    
    def get_region_performance(self) -> Dict[str, float]:
        """Получить выручку по регионам"""
        return dict(self.region_sales)
    
    def get_sales_statistics(self) -> Dict:
        """Получить статистику по продажам"""
        if not self.sales_records:
            return {}
        
        amounts = [record.total_amount for record in self.sales_records]
        
        return {
            'total_sales': len(self.sales_records),
            'total_revenue': self.get_total_revenue(),
            'average_sale': statistics.mean(amounts),
            'median_sale': statistics.median(amounts),
            'min_sale': min(amounts),
            'max_sale': max(amounts),
            'std_deviation': statistics.stdev(amounts) if len(amounts) > 1 else 0
        }
    
    def find_best_performing_product(self) -> Tuple[str, float]:
        """Найти товар с наибольшей выручкой"""
        best_product = ""
        max_revenue = 0
        
        # Проходим по всем продажам и суммируем выручку по товарам
        product_revenues = defaultdict(float)
        for record in self.sales_records:
            product_revenues[record.product] += record.total_amount
        
        for product, revenue in product_revenues.items():
            if revenue > max_revenue:
                max_revenue = revenue
                best_product = product
        
        return best_product, max_revenue
    
    def get_monthly_trends(self) -> Dict[str, float]:
        """Получить ежемесячные тренды (предполагаем формат даты YYYY-MM-DD)"""
        monthly_sales = defaultdict(float)
        
        for record in self.sales_records:
            # Извлекаем месяц из даты (предполагаем формат YYYY-MM-DD)
            month = record.date[:7]  # YYYY-MM
            monthly_sales[month] += record.total_amount
        
        return dict(monthly_sales)
    
    def filter_by_category(self, category: str) -> List[SaleRecord]:
        """Фильтровать продажи по категории"""
        return [record for record in self.sales_records if record.category.lower() == category.lower()]

# Пример использования анализатора продаж
def sales_analyzer_demo():
    analyzer = SalesAnalyzer()
    
    # Создаем тестовые данные
    sample_sales = [
        ("S001", "Ноутбук ProBook", "Электроника", 50000, 2, "2023-01-15", "Москва"),
        ("S002", "Смартфон Galaxy", "Электроника", 30000, 3, "2023-01-16", "Санкт-Петербург"),
        ("S003", "Книга Python", "Книги", 1500, 5, "2023-01-17", "Москва"),
        ("S004", "Ноутбук UltraSlim", "Электроника", 70000, 1, "2023-01-18", "Новосибирск"),
        ("S005", "Наушники SoundMax", "Электроника", 5000, 4, "2023-01-19", "Москва"),
        ("S006", "Книга JavaScript", "Книги", 2000, 3, "2023-01-20", "Екатеринбург"),
        ("S007", "Планшет ViewPad", "Электроника", 25000, 2, "2023-01-21", "Казань"),
        ("S008", "Книга Data Science", "Книги", 3500, 2, "2023-01-22", "Москва"),
    ]
    
    # Добавляем записи
    for sale_data in sample_sales:
        record = SaleRecord(*sale_data)
        analyzer.add_sale(record)
    
    # Выводим результаты анализа
    print("=== Статистика продаж ===")
    stats = analyzer.get_sales_statistics()
    for key, value in stats.items():
        if isinstance(value, float):
            print(f"{key}: {value:.2f}")
        else:
            print(f"{key}: {value}")
    
    print(f"\n=== Топ 3 категории ===")
    top_categories = analyzer.get_top_categories(3)
    for i, (category, revenue) in enumerate(top_categories, 1):
        print(f"{i}. {category}: {revenue:.2f} руб.")
    
    print(f"\n=== Топ 5 товаров ===")
    top_products = analyzer.get_top_products(5)
    for i, (product, quantity) in enumerate(top_products, 1):
        print(f"{i}. {product}: {quantity} шт.")
    
    print(f"\n=== Выручка по регионам ===")
    region_performance = analyzer.get_region_performance()
    for region, revenue in sorted(region_performance.items(), key=lambda x: x[1], reverse=True):
        print(f"{region}: {revenue:.2f} руб.")
    
    print(f"\n=== Лучший товар ===")
    best_product, revenue = analyzer.find_best_performing_product()
    print(f"Товар: {best_product}, Выручка: {revenue:.2f} руб.")
    
    print(f"\n=== Ежемесячные тренды ===")
    monthly_trends = analyzer.get_monthly_trends()
    for month, revenue in monthly_trends.items():
        print(f"{month}: {revenue:.2f} руб.")

sales_analyzer_demo()
```

### Задача 3: Система обработки текста

Разработаем систему для анализа и обработки текста, которая будет использовать различные алгоритмы для извлечения информации из текста.

```python
import re
from typing import Dict, List, Tuple
from collections import Counter, defaultdict
import math

class TextProcessor:
    """Система обработки текста"""
    def __init__(self):
        self.stop_words = {
            'и', 'в', 'на', 'из', 'под', 'а', 'о', 'с', 'к', 'у', 'о', 'за',
            'до', 'по', 'не', 'но', 'же', 'бы', 'что', 'как', 'это', 'он',
            'она', 'оно', 'они', 'мы', 'вы', 'я', 'все', 'всё', 'для',
            'the', 'and', 'or', 'but', 'in', 'on', 'at', 'to', 'for', 'of',
            'with', 'by', 'this', 'that', 'these', 'those', 'i', 'you', 'he',
            'she', 'it', 'we', 'they', 'me', 'him', 'her', 'us', 'them'
        }
    
    def preprocess_text(self, text: str) -> List[str]:
        """Предварительная обработка текста"""
        # Приводим к нижнему регистру
        text = text.lower()
        
        # Удаляем пунктуацию и цифры, оставляем только буквы и пробелы
        text = re.sub(r'[^а-яёa-z\s]', ' ', text)
        
        # Разбиваем на слова
        words = text.split()
        
        # Удаляем стоп-слова
        filtered_words = [word for word in words if word not in self.stop_words and len(word) > 2]
        
        return filtered_words
    
    def get_word_frequency(self, text: str) -> Counter:
        """Получить частоту слов в тексте"""
        words = self.preprocess_text(text)
        return Counter(words)
    
    def get_ngrams(self, text: str, n: int = 2) -> List[str]:
        """Получить n-граммы из текста"""
        words = self.preprocess_text(text)
        ngrams = []
        
        for i in range(len(words) - n + 1):
            ngram = ' '.join(words[i:i+n])
            ngrams.append(ngram)
        
        return ngrams
    
    def calculate_tf_idf(self, documents: List[str]) -> Dict[str, Dict[str, float]]:
        """Рассчитать TF-IDF для коллекции документов"""
        # Сначала получаем все уникальные слова
        all_words = set()
        doc_word_counts = []
        
        for doc in documents:
            words = self.preprocess_text(doc)
            word_count = Counter(words)
            doc_word_counts.append(word_count)
            all_words.update(words)
        
        # Рассчитываем TF-IDF для каждого документа
        tfidf_results = {}
        
        for idx, doc in enumerate(documents):
            doc_tfidf = {}
            total_words = sum(doc_word_counts[idx].values())
            
            for word in all_words:
                # TF (Term Frequency) - частота слова в документе
                tf = doc_word_counts[idx][word] / total_words if total_words > 0 else 0
                
                # IDF (Inverse Document Frequency) - обратная частота документа
                docs_with_word = sum(1 for wc in doc_word_counts if wc[word] > 0)
                idf = math.log(len(documents) / docs_with_word) if docs_with_word > 0 else 0
                
                # TF-IDF
                tfidf = tf * idf
                if tfidf > 0:
                    doc_tfidf[word] = tfidf
            
            tfidf_results[f'document_{idx}'] = doc_tfidf
        
        return tfidf_results
    
    def find_keywords(self, text: str, top_n: int = 10) -> List[Tuple[str, int]]:
        """Найти ключевые слова в тексте"""
        word_freq = self.get_word_frequency(text)
        return word_freq.most_common(top_n)
    
    def calculate_similarity(self, text1: str, text2: str) -> float:
        """Рассчитать схожесть двух текстов по косинусной мере"""
        words1 = set(self.preprocess_text(text1))
        words2 = set(self.preprocess_text(text2))
        
        intersection = words1.intersection(words2)
        union = words1.union(words2)
        
        if len(union) == 0:
            return 0.0
        
        # Коэффициент Жаккара
        similarity = len(intersection) / len(union)
        return similarity
    
    def extract_sentences(self, text: str) -> List[str]:
        """Извлечь предложения из текста"""
        # Разбиваем текст на предложения
        sentences = re.split(r'[.!?]+', text)
        # Удаляем пустые строки и лишние пробелы
        sentences = [s.strip() for s in sentences if s.strip()]
        return sentences
    
    def summarize_text(self, text: str, num_sentences: int = 3) -> str:
        """Создать краткое содержание текста"""
        sentences = self.extract_sentences(text)
        
        if len(sentences) <= num_sentences:
            return '. '.join(sentences) + '.'
        
        # Простая стратегия: берем первые, средние и последние предложения
        step = len(sentences) // num_sentences
        summary_sentences = []
        
        for i in range(0, len(sentences), step):
            if len(summary_sentences) < num_sentences:
                summary_sentences.append(sentences[i])
        
        # Если все равно не набрали нужное количество, добавляем первые
        while len(summary_sentences) < num_sentences and len(summary_sentences) < len(sentences):
            summary_sentences.append(sentences[len(summary_sentences)])
        
        return '. '.join(summary_sentences[:num_sentences]) + '.'

# Пример использования системы обработки текста
def text_processor_demo():
    processor = TextProcessor()
    
    # Примеры текстов
    text1 = """
    Python - это мощный язык программирования, который используется для веб-разработки,
    научных вычислений, анализа данных и многого другого. Python имеет простой синтаксис,
    который делает его отличным выбором для начинающих программистов.
    """
    
    text2 = """
    Язык программирования Python популярен среди разработчиков благодаря своей читаемости
    и простоте. Он поддерживает несколько парадигм программирования, включая объектно-ориентированное
    и функциональное программирование.
    """
    
    text3 = """
    Машинное обучение - это область искусственного интеллекта, которая позволяет системам
    автоматически изучать и улучшаться на основе опыта. Python предоставляет отличные
    библиотеки для машинного обучения.
    """
    
    print("=== Анализ текста 1 ===")
    keywords = processor.find_keywords(text1, 5)
    print("Ключевые слова:")
    for word, count in keywords:
        print(f"  {word}: {count}")
    
    print(f"\nСхожесть текста 1 и 2: {processor.calculate_similarity(text1, text2):.2f}")
    print(f"Схожесть текста 1 и 3: {processor.calculate_similarity(text1, text3):.2f}")
    
    print(f"\n=== TF-IDF анализ ===")
    documents = [text1, text2, text3]
    tfidf_results = processor.calculate_tf_idf(documents)
    
    for doc_name, tfidf in tfidf_results.items():
        print(f"\n{doc_name}:")
        # Показываем топ 3 слова с самым высоким TF-IDF
        top_words = sorted(tfidf.items(), key=lambda x: x[1], reverse=True)[:3]
        for word, score in top_words:
            print(f"  {word}: {score:.3f}")
    
    print(f"\n=== Краткое содержание ===")
    summary = processor.summarize_text(text1, 2)
    print(summary)

text_processor_demo()
```

### Задача 4: Система оптимизации маршрутов

Реализуем упрощенную систему для решения задачи коммивояжера с использованием жадного алгоритма.

```python
import math
from typing import List, Tuple, Dict
from itertools import permutations

class RouteOptimizer:
    """Система оптимизации маршрутов"""
    def __init__(self):
        self.locations: Dict[str, Tuple[float, float]] = {}
    
    def add_location(self, name: str, x: float, y: float):
        """Добавить локацию с координатами"""
        self.locations[name] = (x, y)
    
    def calculate_distance(self, loc1: str, loc2: str) -> float:
        """Рассчитать евклидово расстояние между двумя локациями"""
        x1, y1 = self.locations[loc1]
        x2, y2 = self.locations[loc2]
        return math.sqrt((x2 - x1)**2 + (y2 - y1)**2)
    
    def calculate_route_distance(self, route: List[str]) -> float:
        """Рассчитать общее расстояние маршрута"""
        if len(route) < 2:
            return 0.0
        
        total_distance = 0.0
        for i in range(len(route) - 1):
            total_distance += self.calculate_distance(route[i], route[i+1])
        
        # Добавляем расстояние от последней точки к первой (цикл)
        if len(route) > 2:
            total_distance += self.calculate_distance(route[-1], route[0])
        
        return total_distance
    
    def greedy_nearest_neighbor(self, start_location: str) -> Tuple[List[str], float]:
        """Жадный алгоритм ближайшего соседа"""
        if not self.locations:
            return [], 0.0
        
        unvisited = set(self.locations.keys())
        current = start_location
        route = [current]
        unvisited.remove(current)
        
        while unvisited:
            nearest = min(unvisited, key=lambda x: self.calculate_distance(current, x))
            route.append(nearest)
            unvisited.remove(nearest)
            current = nearest
        
        distance = self.calculate_route_distance(route)
        return route, distance
    
    def brute_force_tsp(self) -> Tuple[List[str], float]:
        """Решение задачи коммивояжера методом полного перебора (для небольшого числа точек)"""
        if len(self.locations) > 8:  # Ограничиваем для производительности
            print("Слишком много локаций для полного перебора")
            return [], float('inf')
        
        locations_list = list(self.locations.keys())
        if len(locations_list) < 2:
            return locations_list, 0.0
        
        min_distance = float('inf')
        best_route = []
        
        # Перебираем все возможные перестановки
        for perm in permutations(locations_list[1:]):  # Фиксируем первую точку
            route = [locations_list[0]] + list(perm)
            distance = self.calculate_route_distance(route)
            
            if distance < min_distance:
                min_distance = distance
                best_route = route
        
        return best_route, min_distance
    
    def print_route_info(self, route: List[str], distance: float, method: str = "Маршрут"):
        """Вывести информацию о маршруте"""
        print(f"\n{method}:")
        print(f"Последовательность: {' -> '.join(route)} -> {route[0]} (цикл)")
        print(f"Общее расстояние: {distance:.2f}")

# Пример использования системы оптимизации маршрутов
def route_optimizer_demo():
    optimizer = RouteOptimizer()
    
    # Добавляем точки (например, города)
    cities_data = [
        ("Москва", 0, 0),
        ("Санкт-Петербург", 650, 100),
        ("Новосибирск", 200, 800),
        ("Екатеринбург", 1200, 400),
        ("Казань", 800, 200),
        ("Нижний Новгород", 400, 150)
    ]
    
    for name, x, y in cities_data:
        optimizer.add_location(name, x, y)
    
    print("=== Оптимизация маршрутов ===")
    
    # Жадный алгоритм
    greedy_route, greedy_distance = optimizer.greedy_nearest_neighbor("Москва")
    optimizer.print_route_info(greedy_route, greedy_distance, "Жадный алгоритм (Москва - старт)")
    
    # Если точек не слишком много, пробуем полный перебор
    if len(optimizer.locations) <= 6:
        optimal_route, optimal_distance = optimizer.brute_force_tsp()
        optimizer.print_route_info(optimal_route, optimal_distance, "Оптимальный маршрут (полный перебор)")
        
        print(f"\nЭффективность жадного алгоритма: {(optimal_distance/greedy_distance)*100:.1f}% от оптимального")

route_optimizer_demo()
```

## Заключение

В этой лекции мы рассмотрели комплексные прикладные задачи, которые демонстрируют применение различных концепций программирования:

1. **Система управления библиотекой** - объединила классы, словари, алгоритмы поиска и управления данными
2. **Анализ данных о продажах** - использовал структуры данных, статистические функции и алгоритмы анализа
3. **Система обработки текста** - применила регулярные выражения, алгоритмы обработки строк и TF-IDF
4. **Система оптимизации маршрутов** - использовала графовые алгоритмы и методы оптимизации

Эти примеры показывают, как различные концепции программирования сочетаются в реальных приложениях. Каждая задача требовала комбинации знаний о:
- Структурах данных (списки, словари, множества)
- Алгоритмах (поиск, сортировка, оптимизация)
- Объектно-ориентированном программировании
- Обработке исключений
- Работе с файлами и данными

В следующей лекции мы подведем итоги курса и подготовимся к итоговой аттестации.
