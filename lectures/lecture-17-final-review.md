# Лекция 17: Подготовка к зачёту / итоговое повторение

## Введение

В этой заключительной лекции мы подводим итоги изучения курса "Основы алгоритмизации и программирования". Мы повторим ключевые темы, обобщим полученные знания и навыки, и подготовимся к итоговой аттестации. Эта лекция служит обзором всего пройденного материала и поможет систематизировать знания по курсу.

## Основное содержание

### Обзор пройденного материала

#### 1. Введение в алгоритмизацию
- Понятие алгоритма: последовательность шагов для решения задачи
- Свойства алгоритмов: дискретность, определённость, конечность, массовость, результативность
- Исполнители алгоритмов: человек, компьютер, робот
- Формы записи алгоритмов: словесная, графическая (блок-схемы), программная
- Этапы решения задач на компьютере: постановка задачи, математическое моделирование, разработка алгоритма, программирование, отладка, использование

#### 2. Знакомство с языком Python
- Назначение Python: универсальный язык программирования
- Среды разработки: IDLE, PyCharm, VS Code, Jupyter Notebook
- Структура программы: импорты, определения, инструкции
- Комментарии: `#` для однострочных, `"""..."""` для многострочных
- Ввод и вывод: `input()`, `print()`
- Соглашения о стиле кода (PEP 8)

#### 3. Типы данных и переменные
- Числовые типы: `int`, `float`
- Строки: `str`
- Логический тип: `bool`
- Операции с типами данных
- Преобразование типов: `int()`, `float()`, `str()`, `bool()`
- Именование переменных

#### 4. Условные конструкции
- Операторы ветвления: `if`, `elif`, `else`
- Логические выражения: `and`, `or`, `not`
- Приоритет операторов
- Вложенные условия

#### 5. Циклы
- Цикл `for`: перебор элементов коллекции
- Цикл `while`: выполнение до выполнения условия
- Операторы `break` и `continue`
- Вложенные циклы

#### 6. Строки и работа с текстом
- Индексация и срезы строк
- Методы строк: `upper()`, `lower()`, `strip()`, `replace()`, `split()`, `join()`
- Форматирование строк: `.format()`, f-строки
- Работа с Unicode

#### 7. Списки и кортежи
- Создание и использование списков
- Методы списков: `append()`, `insert()`, `extend()`, `remove()`, `pop()`, `sort()`, `reverse()`
- Срезы списков
- Кортежи: неизменяемые списки
- Списковые включения (list comprehensions)

#### 8. Словари и множества
- Словари: пары ключ-значение
- Методы словарей: `keys()`, `values()`, `items()`, `get()`, `update()`
- Множества: уникальные элементы
- Операции над множествами: объединение, пересечение, разность

#### 9. Функции
- Определение функций: `def`
- Параметры и аргументы
- Возвращаемые значения: `return`
- Область видимости переменных
- Рекурсивные функции
- Lambda-функции

#### 10. Модули и библиотеки
- Импорт модулей: `import`, `from ... import`
- Стандартные модули: `math`, `random`, `datetime`, `os`, `sys`
- Создание собственных модулей
- Установка сторонних библиотек: `pip`

#### 11. Обработка исключений
- Конструкция `try-except-else-finally`
- Виды исключений: `ValueError`, `TypeError`, `ZeroDivisionError`, `FileNotFoundError`
- Генерация исключений: `raise`

#### 12. Работа с файлами
- Открытие файлов: `open()`
- Режимы: `r`, `w`, `a`, `x`, `b`, `+`
- Чтение и запись: `read()`, `write()`, `readline()`, `readlines()`
- Контекстные менеджеры: `with`

#### 13. Основы ООП
- Классы и объекты
- Атрибуты и методы
- Конструктор: `__init__()`
- Наследование, инкапсуляция, полиморфизм
- Магические методы

#### 14. Алгоритмические конструкции: повторение и обобщение
- Линейные алгоритмы
- Разветвляющиеся алгоритмы
- Циклические алгоритмы
- Структурное программирование

#### 15. Поиск и сортировка (базовые алгоритмы)
- Линейный поиск
- Бинарный поиск
- Сортировка пузырьком
- Сортировка выбором
- Сортировка вставками
- Быстрая сортировка
- Сортировка слиянием

#### 16. Решение прикладных задач
- Комплексные задачи, объединяющие несколько концепций
- Применение структур данных и алгоритмов
- Практические примеры

### Типичные ошибки и рекомендации

#### Частые ошибки начинающих программистов:

1. **Синтаксические ошибки**:
   - Неправильные отступы (Python чувствителен к отступам)
   - Пропущенные двоеточия после `if`, `for`, `while`, `def`, `class`
   - Несоответствие открывающих и закрывающих скобок, кавычек

2. **Логические ошибки**:
   - Неправильные условия в `if` и `while`
   - Ошибки в индексации (выход за границы массива)
   - Неправильное использование логических операторов

3. **Ошибки при работе с типами данных**:
   - Попытка выполнить операции с несовместимыми типами
   - Неправильное преобразование типов

4. **Ошибки при работе с файлами**:
   - Забытые `close()` при открытии файлов
   - Несуществующие пути к файлам
   - Неправильные режимы открытия файлов

#### Рекомендации по написанию кода:

1. **Следуйте PEP 8**:
   - Используйте 4 пробела на каждый уровень отступа
   - Имена переменных в `snake_case`
   - Имена классов в `CamelCase`
   - Константы в `UPPER_CASE`

2. **Пишите читаемый код**:
   - Используйте понятные имена переменных и функций
   - Добавляйте комментарии к сложным участкам кода
   - Разбивайте сложные задачи на более простые функции

3. **Тестируйте код**:
   - Проверяйте граничные условия
   - Используйте разные входные данные
   - Обрабатывайте возможные исключения

4. **Используйте отладку**:
   - Временные `print()` для отслеживания значений переменных
   - Отладчики в IDE
   - Тестирование отдельных функций

### Примеры решения комплексных задач

#### Задача: Система управления студентами

```python
from datetime import datetime
from typing import List, Dict, Optional

class Student:
    """Класс для представления студента"""
    def __init__(self, student_id: str, name: str, email: str, major: str):
        self.student_id = student_id
        self.name = name
        self.email = email
        self.major = major
        self.grades = {}
        self.enrolled_courses = []
        self.enrollment_date = datetime.now()
    
    def add_grade(self, subject: str, grade: float):
        """Добавить оценку по предмету"""
        if subject not in self.grades:
            self.grades[subject] = []
        self.grades[subject].append(grade)
    
    def get_average_grade(self, subject: str = None) -> float:
        """Получить средний балл"""
        if subject:
            if subject in self.grades and self.grades[subject]:
                return sum(self.grades[subject]) / len(self.grades[subject])
            return 0.0
        else:
            all_grades = []
            for grades_list in self.grades.values():
                all_grades.extend(grades_list)
            return sum(all_grades) / len(all_grades) if all_grades else 0.0

class Course:
    """Класс для представления курса"""
    def __init__(self, course_code: str, title: str, credits: int, instructor: str):
        self.course_code = course_code
        self.title = title
        self.credits = credits
        self.instructor = instructor
        self.students = []
        self.max_capacity = 30
    
    def enroll_student(self, student: Student) -> bool:
        """Записать студента на курс"""
        if len(self.students) >= self.max_capacity:
            return False
        if student not in self.students:
            self.students.append(student)
            if self.course_code not in student.enrolled_courses:
                student.enrolled_courses.append(self.course_code)
            return True
        return False

class StudentManagementSystem:
    """Система управления студентами"""
    def __init__(self):
        self.students: Dict[str, Student] = {}
        self.courses: Dict[str, Course] = {}
        self.enrollment_records = []
    
    def add_student(self, student: Student):
        """Добавить студента в систему"""
        self.students[student.student_id] = student
    
    def add_course(self, course: Course):
        """Добавить курс в систему"""
        self.courses[course.course_code] = course
    
    def enroll_student_in_course(self, student_id: str, course_code: str) -> bool:
        """Записать студента на курс"""
        if student_id not in self.students or course_code not in self.courses:
            return False
        
        student = self.students[student_id]
        course = self.courses[course_code]
        
        if course.enroll_student(student):
            self.enrollment_records.append({
                'student_id': student_id,
                'course_code': course_code,
                'enrollment_date': datetime.now()
            })
            return True
        return False
    
    def get_top_students(self, n: int = 5) -> List[Student]:
        """Получить топ N студентов по среднему баллу"""
        students_with_avg = [(student, student.get_average_grade()) 
                            for student in self.students.values()]
        sorted_students = sorted(students_with_avg, 
                                key=lambda x: x[1], reverse=True)
        return [student for student, avg in sorted_students[:n]]
    
    def get_course_statistics(self, course_code: str) -> Dict:
        """Получить статистику по курсу"""
        if course_code not in self.courses:
            return {}
        
        course = self.courses[course_code]
        stats = {
            'course_code': course.course_code,
            'title': course.title,
            'enrolled_students': len(course.students),
            'capacity': course.max_capacity,
            'occupancy_rate': len(course.students) / course.max_capacity * 100
        }
        
        # Средний балл по курсу (если есть оценки)
        all_grades = []
        for student in course.students:
            if course_code in student.grades:
                all_grades.extend(student.grades[course_code])
        
        if all_grades:
            stats['average_grade'] = sum(all_grades) / len(all_grades)
        else:
            stats['average_grade'] = 0.0
        
        return stats

# Пример использования системы
def student_management_demo():
    sms = StudentManagementSystem()
    
    # Создаем студентов
    students_data = [
        ("S001", "Иванов Иван", "ivanov@example.com", "Информатика"),
        ("S002", "Петрова Мария", "petrova@example.com", "Математика"),
        ("S003", "Сидоров Алексей", "sidorov@example.com", "Физика"),
        ("S004", "Кузнецова Анна", "kuznetsova@example.com", "Информатика"),
        ("S005", "Волков Дмитрий", "volkov@example.com", "Математика")
    ]
    
    for student_id, name, email, major in students_data:
        student = Student(student_id, name, email, major)
        sms.add_student(student)
    
    # Создаем курсы
    courses_data = [
        ("CS101", "Введение в программирование", 4, "Доцент Смирнов"),
        ("MATH201", "Математический анализ", 5, "Профессор Козлов"),
        ("PHYS301", "Физика полупроводников", 4, "Доцент Волкова")
    ]
    
    for course_code, title, credits, instructor in courses_data:
        course = Course(course_code, title, credits, instructor)
        sms.add_course(course)
    
    # Записываем студентов на курсы
    sms.enroll_student_in_course("S001", "CS101")
    sms.enroll_student_in_course("S001", "MATH201")
    sms.enroll_student_in_course("S002", "MATH201")
    sms.enroll_student_in_course("S003", "PHYS301")
    sms.enroll_student_in_course("S004", "CS101")
    sms.enroll_student_in_course("S005", "MATH201")
    
    # Добавляем оценки
    sms.students["S001"].add_grade("CS101", 5)
    sms.students["S001"].add_grade("CS101", 4)
    sms.students["S001"].add_grade("MATH201", 5)
    sms.students["S002"].add_grade("MATH201", 4)
    sms.students["S002"].add_grade("MATH201", 5)
    sms.students["S003"].add_grade("PHYS301", 4)
    sms.students["S004"].add_grade("CS101", 5)
    sms.students["S004"].add_grade("CS101", 5)
    sms.students["S005"].add_grade("MATH201", 4)
    sms.students["S005"].add_grade("MATH201", 4)
    
    # Выводим результаты
    print("=== Топ студентов ===")
    top_students = sms.get_top_students(3)
    for i, student in enumerate(top_students, 1):
        avg_grade = student.get_average_grade()
        print(f"{i}. {student.name} (ID: {student.student_id}): {avg_grade:.2f}")
    
    print("\n=== Статистика по курсу CS101 ===")
    cs_stats = sms.get_course_statistics("CS101")
    for key, value in cs_stats.items():
        if isinstance(value, float):
            print(f"{key}: {value:.2f}")
        else:
            print(f"{key}: {value}")

student_management_demo()
```

### Подготовка к зачёту

#### Темы для повторения:

1. **Основы синтаксиса Python**:
   - Переменные и типы данных
   - Условные операторы
   - Циклы
   - Функции

2. **Структуры данных**:
   - Списки, кортежи, словари, множества
   - Методы и операции с ними
   - Списковые включения

3. **Объектно-ориентированное программирование**:
   - Классы и объекты
   - Наследование и полиморфизм
   - Инкапсуляция

4. **Работа с файлами**:
   - Открытие, чтение, запись
   - Контекстные менеджеры

5. **Обработка исключений**:
   - Конструкция try-except
   - Виды исключений
   - Генерация исключений

6. **Алгоритмы**:
   - Поиск и сортировка
   - Рекурсия
   - Сложность алгоритмов

#### Примеры задач для подготовки:

1. **Работа со строками**: Написать функцию, которая проверяет, является ли строка палиндромом.

2. **Работа со списками**: Реализовать алгоритм сортировки выбором.

3. **Файлы**: Написать программу, которая подсчитывает количество слов в текстовом файле.

4. **Классы**: Создать класс "Книга" с методами для управления состоянием книги.

5. **Исключения**: Написать безопасную функцию деления, обрабатывающую деление на ноль.

6. **Алгоритмы**: Реализовать бинарный поиск в отсортированном массиве.

### Рекомендации по подготовке

1. **Практика**: Решайте как можно больше задач разного уровня сложности
2. **Анализ кода**: Изучайте чужой код, анализируйте, как он работает
3. **Тестирование**: Проверяйте код с разными входными данными
4. **Документирование**: Учитесь писать понятные комментарии и docstring
5. **Работа в проекте**: Попробуйте создать небольшой проект, объединяющий несколько концепций

## Заключение

Курс "Основы алгоритмизации и программирования" завершен. За время обучения вы:

- Освоили основы языка программирования Python
- Изучили ключевые концепции программирования: переменные, типы данных, структуры управления, функции
- Научились работать с различными структурами данных
- Познакомились с объектно-ориентированным программированием
- Освоили алгоритмы поиска и сортировки
- Научились решать прикладные задачи, объединяя различные концепции

Эти знания составляют основу для дальнейшего изучения программирования и смежных дисциплин. Помните, что программирование - это навык, который развивается с практикой. Регулярно пишите код, решайте задачи, экспериментируйте с новыми идеями.

Успешной сдачи зачёта и дальнейших успехов в изучении программирования!
