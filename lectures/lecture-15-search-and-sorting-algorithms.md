# Лекция 15: Поиск и сортировка (базовые алгоритмы)

## Введение

Поиск и сортировка - это две фундаментальные задачи в программировании, которые встречаются почти в каждой области информатики. Алгоритмы поиска позволяют находить элементы в коллекциях данных, а алгоритмы сортировки упорядочивают элементы для более эффективной обработки. В этой лекции мы рассмотрим базовые алгоритмы поиска и сортировки, их реализацию на Python и анализ эффективности.

## Основное содержание

### Алгоритмы поиска

#### Линейный (последовательный) поиск

Линейный поиск - это простейший алгоритм поиска, который последовательно проверяет каждый элемент в коллекции до тех пор, пока не найдет искомое значение или не достигнет конца коллекции.

```python
def linear_search(arr, target):
    """
    Линейный поиск элемента в массиве
    Возвращает индекс элемента или -1, если элемент не найден
    """
    for i in range(len(arr)):
        if arr[i] == target:
            return i  # Возвращаем индекс найденного элемента
    return -1  # Элемент не найден

# Пример использования
numbers = [64, 34, 25, 12, 22, 11, 90]
target = 22
result = linear_search(numbers, target)

if result != -1:
    print(f"Элемент {target} найден по индексу {result}")
else:
    print(f"Элемент {target} не найден")

# Временная сложность: O(n)
# Пространственная сложность: O(1)
```

#### Бинарный поиск

Бинарный поиск работает только с отсортированными массивами. Он многократно делит пополам область поиска, сравнивая целевое значение со средним элементом.

```python
def binary_search(arr, target):
    """
    Бинарный поиск элемента в отсортированном массиве
    Возвращает индекс элемента или -1, если элемент не найден
    """
    left, right = 0, len(arr) - 1
    
    while left <= right:
        mid = (left + right) // 2
        
        if arr[mid] == target:
            return mid
        elif arr[mid] < target:
            left = mid + 1  # Искомый элемент в правой половине
        else:
            right = mid - 1  # Искомый элемент в левой половине
    
    return -1  # Элемент не найден

# Пример использования
sorted_numbers = [11, 12, 25, 34, 64, 90]
target = 25
result = binary_search(sorted_numbers, target)

if result != -1:
    print(f"Элемент {target} найден по индексу {result}")
else:
    print(f"Элемент {target} не найден")

# Временная сложность: O(log n)
# Пространственная сложность: O(1)
```

#### Рекурсивная версия бинарного поиска

```python
def binary_search_recursive(arr, target, left=0, right=None):
    """
    Рекурсивная версия бинарного поиска
    """
    if right is None:
        right = len(arr) - 1
    
    if left > right:
        return -1  # Элемент не найден
    
    mid = (left + right) // 2
    
    if arr[mid] == target:
        return mid
    elif arr[mid] < target:
        return binary_search_recursive(arr, target, mid + 1, right)
    else:
        return binary_search_recursive(arr, target, left, mid - 1)

# Пример использования
result = binary_search_recursive(sorted_numbers, 64)
print(f"Рекурсивный бинарный поиск: элемент 64 найден по индексу {result}")
```

### Алгоритмы сортировки

#### Сортировка пузырьком (Bubble Sort)

Сортировка пузырьком многократно проходит по списку, сравнивает соседние элементы и меняет их местами, если они находятся в неправильном порядке.

```python
def bubble_sort(arr):
    """
    Сортировка пузырьком
    """
    n = len(arr)
    # Проходим по всем элементам
    for i in range(n):
        # Флаг для оптимизации - если за проход не было обменов, то массив отсортирован
        swapped = False
        
        # Последние i элементов уже отсортированы
        for j in range(0, n - i - 1):
            # Если текущий элемент больше следующего, меняем их местами
            if arr[j] > arr[j + 1]:
                arr[j], arr[j + 1] = arr[j + 1], arr[j]
                swapped = True
        
        # Если не было обменов, массив уже отсортирован
        if not swapped:
            break
    
    return arr

# Пример использования
numbers = [64, 34, 25, 12, 22, 11, 90]
print(f"До сортировки: {numbers}")
sorted_numbers = bubble_sort(numbers.copy())
print(f"После сортировки: {sorted_numbers}")

# Временная сложность: O(n²) в худшем случае, O(n) в лучшем случае
# Пространственная сложность: O(1)
```

#### Сортировка выбором (Selection Sort)

Сортировка выбором находит минимальный элемент в неотсортированной части массива и помещает его в начало.

```python
def selection_sort(arr):
    """
    Сортировка выбором
    """
    n = len(arr)
    
    # Проходим по всем элементам
    for i in range(n):
        # Находим индекс минимального элемента в оставшейся части
        min_idx = i
        for j in range(i + 1, n):
            if arr[j] < arr[min_idx]:
                min_idx = j
        
        # Меняем местами минимальный элемент с первым элементом в неотсортированной части
        arr[i], arr[min_idx] = arr[min_idx], arr[i]
    
    return arr

# Пример использования
numbers = [64, 34, 25, 12, 22, 11, 90]
print(f"До сортировки: {numbers}")
sorted_numbers = selection_sort(numbers.copy())
print(f"После сортировки: {sorted_numbers}")

# Временная сложность: O(n²)
# Пространственная сложность: O(1)
```

#### Сортировка вставками (Insertion Sort)

Сортировка вставками строит отсортированный массив по одному элементу за раз, перемещая каждый новый элемент на правильное место среди уже отсортированных элементов.

```python
def insertion_sort(arr):
    """
    Сортировка вставками
    """
    # Начинаем со второго элемента (первый считается отсортированным)
    for i in range(1, len(arr)):
        key = arr[i]  # Элемент для вставки
        j = i - 1     # Индекс последнего элемента в отсортированной части
        
        # Сдвигаем элементы, которые больше key, вправо
        while j >= 0 and arr[j] > key:
            arr[j + 1] = arr[j]
            j -= 1
        
        # Вставляем key на правильное место
        arr[j + 1] = key
    
    return arr

# Пример использования
numbers = [64, 34, 25, 12, 22, 11, 90]
print(f"До сортировки: {numbers}")
sorted_numbers = insertion_sort(numbers.copy())
print(f"После сортировки: {sorted_numbers}")

# Временная сложность: O(n²) в худшем случае, O(n) в лучшем случае
# Пространственная сложность: O(1)
```

#### Быстрая сортировка (Quick Sort)

Быстрая сортировка - это эффективный алгоритм сортировки, который использует принцип "разделяй и властвуй". Она выбирает опорный элемент и разделяет массив на две части: элементы меньше опорного и элементы больше или равны опорному.

```python
def quick_sort(arr):
    """
    Быстрая сортировка (рекурсивная версия)
    """
    if len(arr) <= 1:
        return arr
    
    pivot = arr[len(arr) // 2]  # Выбираем опорный элемент (середину)
    
    # Разделяем массив на три части
    left = [x for x in arr if x < pivot]      # Элементы меньше опорного
    middle = [x for x in arr if x == pivot]   # Элементы, равные опорному
    right = [x for x in arr if x > pivot]     # Элементы больше опорного
    
    # Рекурсивно сортируем левую и правую части, затем объединяем
    return quick_sort(left) + middle + quick_sort(right)

# Альтернативная реализация с сортировкой на месте
def quick_sort_inplace(arr, low=0, high=None):
    """
    Быстрая сортировка с сортировкой на месте
    """
    if high is None:
        high = len(arr) - 1
    
    if low < high:
        # Разделяем массив и получаем индекс опорного элемента
        pivot_index = partition(arr, low, high)
        
        # Рекурсивно сортируем элементы до и после опорного
        quick_sort_inplace(arr, low, pivot_index - 1)
        quick_sort_inplace(arr, pivot_index + 1, high)

def partition(arr, low, high):
    """
    Функция разделения для быстрой сортировки
    """
    pivot = arr[high]  # Опорный элемент - последний элемент
    i = low - 1        # Индекс для меньших элементов
    
    for j in range(low, high):
        # Если текущий элемент меньше или равен опорному
        if arr[j] <= pivot:
            i += 1
            arr[i], arr[j] = arr[j], arr[i]  # Меняем местами
    
    # Ставим опорный элемент на правильное место
    arr[i + 1], arr[high] = arr[high], arr[i + 1]
    return i + 1

# Пример использования
numbers = [64, 34, 25, 12, 22, 11, 90]
print(f"До сортировки: {numbers}")
sorted_numbers = quick_sort(numbers.copy())
print(f"После сортировки: {sorted_numbers}")

# Временная сложность: O(n log n) в среднем случае, O(n²) в худшем случае
# Пространственная сложность: O(log n) из-за рекурсии
```

#### Сортировка слиянием (Merge Sort)

Сортировка слиянием также использует принцип "разделяй и властвуй". Она делит массив на половины, рекурсивно сортирует каждую половину, а затем объединяет отсортированные половины.

```python
def merge_sort(arr):
    """
    Сортировка слиянием
    """
    if len(arr) <= 1:
        return arr
    
    # Делим массив на две половины
    mid = len(arr) // 2
    left = merge_sort(arr[:mid])
    right = merge_sort(arr[mid:])
    
    # Сливаем отсортированные половины
    return merge(left, right)

def merge(left, right):
    """
    Функция слияния двух отсортированных массивов
    """
    result = []
    i = j = 0
    
    # Сравниваем элементы из обеих половин и добавляем меньший в результат
    while i < len(left) and j < len(right):
        if left[i] <= right[j]:
            result.append(left[i])
            i += 1
        else:
            result.append(right[j])
            j += 1
    
    # Добавляем оставшиеся элементы
    result.extend(left[i:])
    result.extend(right[j:])
    
    return result

# Пример использования
numbers = [64, 34, 25, 12, 22, 11, 90]
print(f"До сортировки: {numbers}")
sorted_numbers = merge_sort(numbers.copy())
print(f"После сортировки: {sorted_numbers}")

# Временная сложность: O(n log n) в худшем, среднем и лучшем случаях
# Пространственная сложность: O(n)
```

### Сравнение алгоритмов

| Алгоритм | Лучший случай | Средний случай | Худший случай | Память | Устойчивость |
|----------|---------------|----------------|---------------|---------|--------------|
| Линейный поиск | O(1) | O(n) | O(1) | - |
| Бинарный поиск | O(1) | O(log n) | O(log n) | O(1) | - |
| Сортировка пузырьком | O(n) | O(n²) | O(n²) | O(1) | Да |
| Сортировка выбором | O(n²) | O(n²) | O(n²) | O(1) | Нет |
| Сортировка вставками | O(n) | O(n²) | O(n²) | O(1) | Да |
| Быстрая сортировка | O(n log n) | O(n log n) | O(n²) | O(log n) | Нет |
| Сортировка слиянием | O(n log n) | O(n log n) | O(n log n) | O(n) | Да |

**Устойчивость** - это свойство алгоритма сортировки, при котором относительный порядок элементов с одинаковыми ключами сохраняется после сортировки.

### Практические примеры

#### Пример 1: Поиск в телефонной книге

```python
class PhoneBook:
    def __init__(self):
        self.contacts = []  # Список кортежей (имя, телефон)
    
    def add_contact(self, name, phone):
        """Добавить контакт"""
        self.contacts.append((name, phone))
        # Сортируем по имени после добавления
        self.contacts.sort(key=lambda x: x[0])
    
    def linear_search(self, name):
        """Линейный поиск контакта по имени"""
        for i, (contact_name, phone) in enumerate(self.contacts):
            if contact_name.lower() == name.lower():
                return i, phone
        return -1, None
    
    def binary_search(self, name):
        """Бинарный поиск контакта по имени"""
        left, right = 0, len(self.contacts) - 1
        
        while left <= right:
            mid = (left + right) // 2
            mid_name = self.contacts[mid][0].lower()
            target_name = name.lower()
            
            if mid_name == target_name:
                return mid, self.contacts[mid][1]
            elif mid_name < target_name:
                left = mid + 1
            else:
                right = mid - 1
        
        return -1, None

# Пример использования
phonebook = PhoneBook()
contacts_data = [
    ("Иванов", "+7 (111) 111-11-11"),
    ("Петров", "+7 (222) 222-22-22"),
    ("Сидоров", "+7 (333) 333-33-33"),
    ("Алексеев", "+7 (444) 444-44-44"),
    ("Борисов", "+7 (555) 555-55-55")
]

for name, phone in contacts_data:
    phonebook.add_contact(name, phone)

# Поиск контакта
name_to_find = "Петров"
index, phone = phonebook.binary_search(name_to_find)
if index != -1:
    print(f"Контакт {name_to_find}: {phone}")
else:
    print(f"Контакт {name_to_find} не найден")
```

#### Пример 2: Сортировка студентов по баллам

```python
class Student:
    def __init__(self, name, grade):
        self.name = name
        self.grade = grade
    
    def __repr__(self):
        return f"Student('{self.name}', {self.grade})"

def sort_students_by_grade(students):
    """Сортировка студентов по оценке (от большей к меньшей)"""
    # Используем сортировку вставками для небольших списков
    for i in range(1, len(students)):
        current_student = students[i]
        j = i - 1
        
        # Сравниваем по оценке (в порядке убывания)
        while j >= 0 and students[j].grade < current_student.grade:
            students[j + 1] = students[j]
            j -= 1
        
        students[j + 1] = current_student
    
    return students

def sort_students_by_name(students):
    """Сортировка студентов по имени (алфавитный порядок)"""
    # Используем быструю сортировку
    if len(students) <= 1:
        return students
    
    pivot = students[len(students) // 2]
    left = [s for s in students if s.name < pivot.name]
    middle = [s for s in students if s.name == pivot.name]
    right = [s for s in students if s.name > pivot.name]
    
    return sort_students_by_name(left) + middle + sort_students_by_name(right)

# Пример использования
students = [
    Student("Иванов", 4.5),
    Student("Петров", 4.8),
    Student("Сидоров", 3.9),
    Student("Алексеев", 5.0),
    Student("Борисов", 4.2)
]

print("Студенты до сортировки:")
for student in students:
    print(student)

# Сортировка по оценке
sorted_by_grade = sort_students_by_grade(students.copy())
print("\nСтуденты, отсортированные по оценке:")
for student in sorted_by_grade:
    print(student)

# Сортировка по имени
sorted_by_name = sort_students_by_name(students.copy())
print("\nСтуденты, отсортированные по имени:")
for student in sorted_by_name:
    print(student)
```

#### Пример 3: Сравнение эффективности алгоритмов сортировки

```python
import time
import random

def time_sorting_algorithm(sort_func, data, algorithm_name):
    """Измеряет время выполнения алгоритма сортировки"""
    data_copy = data.copy()
    start_time = time.time()
    
    if algorithm_name == "quick_sort_inplace":
        # Для inplace-алгоритмов передаем массив по ссылке
        sort_func(data_copy)
    else:
        sorted_data = sort_func(data_copy)
    
    end_time = time.time()
    return end_time - start_time

def generate_random_data(size):
    """Генерирует случайные данные для тестирования"""
    return [random.randint(1, 1000) for _ in range(size)]

# Тестирование на разных размерах данных
sizes = [100, 500, 1000]
algorithms = [
    ("Bubble Sort", bubble_sort),
    ("Selection Sort", selection_sort),
    ("Insertion Sort", insertion_sort),
    ("Quick Sort", quick_sort),
    ("Merge Sort", merge_sort)
]

print("Сравнение времени выполнения алгоритмов сортировки:")
print("-" * 60)

for size in sizes:
    print(f"\nРазмер данных: {size}")
    test_data = generate_random_data(size)
    
    for name, func in algorithms:
        # Для inplace-сортировки создаем копию каждый раз
        if name == "Quick Sort (inplace)":
            execution_time = time_sorting_algorithm(
                lambda x: quick_sort_inplace(x), 
                test_data.copy(), 
                "quick_sort_inplace"
            )
        else:
            execution_time = time_sorting_algorithm(func, test_data, name)
        
        print(f"{name:15}: {execution_time:.6f} сек")
```

## Заключение

В этой лекции мы рассмотрели основные алгоритмы поиска и сортировки:

1. **Алгоритмы поиска**:
   - Линейный поиск: прост, но медленный (O(n))
   - Бинарный поиск: быстрый, но требует отсортированный массив (O(log n))

2. **Алгоритмы сортировки**:
   - Сортировка пузырьком: проста для понимания, но неэффективна (O(n²))
   - Сортировка выбором: также O(n²), но с меньшим количеством обменов
   - Сортировка вставками: эффективна для маленьких или почти отсортированных массивов
   - Быстрая сортировка: очень эффективна в среднем случае (O(n log n))
   - Сортировка слиянием: стабильно эффективна во всех случаях (O(n log n))

Понимание этих алгоритмов важно для выбора правильного инструмента для решения конкретной задачи. В следующей лекции мы рассмотрим решение прикладных задач, применяя изученные алгоритмы и структуры данных.
