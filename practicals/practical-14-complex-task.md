# Практическая работа 14: Комплексная задача

## Цель работы

Создать полнофункциональное приложение, объединяющее несколько концепций программирования: переменные, типы данных, условные операторы, циклы, функции, словари/списки, обработку исключений и файловый ввод-вывод. Задача представляет собой мини-проект, например, систему учета студентов или дневник расходов.

## Вариант задания: Система учета студентов

Разработать программу, которая позволяет вести учет студентов и их оценок. Программа должна включать следующие функции:
- Добавление новых студентов
- Добавление оценок студентам
- Просмотр информации о студентах
- Расчет среднего балла
- Сохранение и загрузка данных из файла

## Теоретическая часть

Комплексные задачи требуют применения нескольких концепций программирования одновременно. В этой работе мы будем использовать:
- Структуры данных (списки, словари)
- Функции для структурирования кода
- Условные операторы для ветвления
- Циклы для повторяющихся операций
- Обработку исключений для надежности
- Файловый ввод-вывод для сохранения данных

## Практическое задание

### Задание 1: Создание основной структуры программы

Создайте основную структуру программы с меню и основными функциями:

```python
def add_student(students, name, age, major):
    """Добавляет нового студента в список"""
    student = {
        "name": name,
        "age": age,
        "major": major,
        "grades": [],
        "enrollment_date": datetime.now().strftime("%Y-%m-%d")
    }
    students.append(student)
    return True

def add_grade(students, name, subject, grade):
    """Добавляет оценку студенту по предмету"""
    for student in students:
        if student["name"].lower() == name.lower():
            if "subjects" not in student:
                student["subjects"] = {}
            if subject not in student["subjects"]:
                student["subjects"][subject] = []
            student["subjects"][subject].append(grade)
            return True
    return False

def calculate_average_grade(student):
    """Вычисляет средний балл студента"""
    if "subjects" not in student or not student["subjects"]:
        return 0
    
    all_grades = []
    for grades in student["subjects"].values():
        all_grades.extend(grades)
    
    if not all_grades:
        return 0
    
    return sum(all_grades) / len(all_grades)

def find_student(students, name):
    """Находит студента по имени"""
    for student in students:
        if student["name"].lower() == name.lower():
            return student
    return None

def display_all_students(students):
    """Выводит информацию о всех студентах"""
    if not students:
        print("Нет студентов в системе")
        return
    
    for i, student in enumerate(students, 1):
        avg_grade = calculate_average_grade(student)
        print(f"{i}. {student['name']}, {student['age']} лет, {student['major']}")
        print(f"   Средний балл: {avg_grade:.2f}")
        if "subjects" in student:
            print(f"   Предметы: {', '.join(student['subjects'].keys())}")
        print()

def save_to_file(students, filename):
    """Сохраняет данные студентов в файл"""
    try:
        with open(filename, 'w', encoding='utf-8') as f:
            json.dump(students, f, ensure_ascii=False, indent=2)
        print(f"Данные сохранены в {filename}")
        return True
    except Exception as e:
        print(f"Ошибка при сохранении в файл: {e}")
        return False

def load_from_file(filename):
    """Загружает данные студентов из файла"""
    try:
        with open(filename, 'r', encoding='utf-8') as f:
            students = json.load(f)
        print(f"Данные загружены из {filename}")
        return students
    except FileNotFoundError:
        print(f"Файл {filename} не найден, создаем пустой список")
        return []
    except Exception as e:
        print(f"Ошибка при загрузке из файла: {e}")
        return []

# Основная программа
import json
from datetime import datetime

students = []
filename = "students_data.json"

# Загружаем данные из файла при запуске
students = load_from_file(filename)

while True:
    print("\n=== Система учета студентов ===")
    print("1. Добавить студента")
    print("2. Добавить оценку")
    print("3. Просмотреть всех студентов")
    print("4. Найти студента")
    print("5. Просмотреть информацию о студенте")
    print("6. Сохранить данные")
    print("7. Загрузить данные")
    print("0. Выход")
    
    choice = input("Выберите действие: ")
    
    if choice == "1":
        name = input("Введите имя студента: ")
        age = int(input("Введите возраст: "))
        major = input("Введите специальность: ")
        
        if add_student(students, name, age, major):
            print("Студент добавлен")
        else:
            print("Ошибка при добавлении студента")
    
    elif choice == "2":
        name = input("Введите имя студента: ")
        subject = input("Введите название предмета: ")
        try:
            grade = float(input("Введите оценку: "))
            if 0 <= grade <= 10:
                if add_grade(students, name, subject, grade):
                    print("Оценка добавлена")
                else:
                    print("Студент не найден")
            else:
                print("Оценка должна быть от 0 до 10")
        except ValueError:
            print("Некорректный формат оценки")
    
    elif choice == "3":
        display_all_students(students)
    
    elif choice == "4":
        name = input("Введите имя студента для поиска: ")
        student = find_student(students, name)
        if student:
            avg_grade = calculate_average_grade(student)
            print(f"Найден: {student['name']}, {student['age']} лет, {student['major']}")
            print(f"Средний балл: {avg_grade:.2f}")
        else:
            print("Студент не найден")
    
    elif choice == "5":
        name = input("Введите имя студента: ")
        student = find_student(students, name)
        if student:
            print(f"Имя: {student['name']}")
            print(f"Возраст: {student['age']}")
            print(f"Специальность: {student['major']}")
            print(f"Дата поступления: {student['enrollment_date']}")
            avg_grade = calculate_average_grade(student)
            print(f"Средний балл: {avg_grade:.2f}")
            
            if "subjects" in student and student["subjects"]:
                print("Оценки по предметам:")
                for subject, grades in student["subjects"].items():
                    subject_avg = sum(grades) / len(grades) if grades else 0
                    print(f"  {subject}: {grades} (средний: {subject_avg:.2f})")
        else:
            print("Студент не найден")
    
    elif choice == "6":
        save_to_file(students, filename)
    
    elif choice == "7":
        students = load_from_file(filename)
    
    elif choice == "0":
        # Сохраняем перед выходом
        save_to_file(students, filename)
        print("До свидания!")
        break
    
    else:
        print("Неверный выбор")
```

---

### Задание 2: Улучшение программы

Добавьте в программу дополнительные функции:
- Удаление студентов
- Фильтрация студентов по специальности
- Поиск студентов с высоким средним баллом (> 4.0)
- Экспорт отчета в текстовый файл

**Код для выполнения:**
```python
def remove_student(students, name):
    """Удаляет студента из списка"""
    for i, student in enumerate(students):
        if student["name"].lower() == name.lower():
            del students[i]
            return True
    return False

def filter_by_major(students, major):
    """Фильтрует студентов по специальности"""
    return [student for student in students if student["major"].lower() == major.lower()]

def find_high_performers(students, threshold=4.0):
    """Находит студентов с высоким средним баллом"""
    high_performers = []
    for student in students:
        avg_grade = calculate_average_grade(student)
        if avg_grade >= threshold:
            high_performers.append((student, avg_grade))
    return high_performers

def export_report(students, filename):
    """Экспортирует отчет о студентах в текстовый файл"""
    try:
        with open(filename, 'w', encoding='utf-8') as f:
            f.write("Отчет о студентах\n")
            f.write("=" * 50 + "\n")
            f.write(f"Всего студентов: {len(students)}\n\n")
            
            for i, student in enumerate(students, 1):
                f.write(f"{i}. {student['name']}\n")
                f.write(f"   Возраст: {student['age']}\n")
                f.write(f"   Специальность: {student['major']}\n")
                avg_grade = calculate_average_grade(student)
                f.write(f"   Средний балл: {avg_grade:.2f}\n")
                
                if "subjects" in student:
                    f.write("   Предметы и оценки:\n")
                    for subject, grades in student["subjects"].items():
                        f.write(f"     {subject}: {grades}\n")
                f.write("\n")
        
        print(f"Отчет экспортирован в {filename}")
        return True
    except Exception as e:
        print(f"Ошибка при экспорте отчета: {e}")
        return False

# Добавляем новые опции в меню
# (код основного цикла с дополнительными опциями)
```

---

### Задание 3: Обработка ошибок и валидация данных

Улучшите программу, добавив обработку ошибок и валидацию входных данных:

```python
def validate_student_data(name, age, major):
    """Проверяет корректность данных студента"""
    errors = []
    
    if not name or len(name.strip()) < 2:
        errors.append("Имя должно содержать хотя бы 2 символа")
    
    if not isinstance(age, int) or age < 16 or age > 100:
        errors.append("Возраст должен быть целым числом от 16 до 100")
    
    if not major or len(major.strip()) < 2:
        errors.append("Специальность должна содержать хотя бы 2 символа")
    
    return errors

def validate_grade(grade):
    """Проверяет корректность оценки"""
    try:
        grade = float(grade)
        if 0 <= grade <= 10:
            return True, grade
        else:
            return False, "Оценка должна быть от 0 до 10"
    except ValueError:
        return False, "Оценка должна быть числом"

# Используем валидацию в основной программе
def safe_add_student(students):
    """Безопасное добавление студента с проверкой данных"""
    name = input("Введите имя студента: ").strip()
    try:
        age = int(input("Введите возраст: "))
    except ValueError:
        print("Возраст должен быть числом")
        return False
    
    major = input("Введите специальность: ").strip()
    
    # Проверяем данные
    validation_errors = validate_student_data(name, age, major)
    if validation_errors:
        print("Ошибки валидации:")
        for error in validation_errors:
            print(f"- {error}")
        return False
    
    return add_student(students, name, age, major)
```

---

### Задание 4: Расширенная функциональность

Добавьте в программу возможность:
- Сортировки студентов по среднему баллу
- Статистики по предметам
- Импорта данных из CSV

```python
def sort_students_by_grade(students, reverse=True):
    """Сортирует студентов по среднему баллу"""
    return sorted(students, key=calculate_average_grade, reverse=reverse)

def subject_statistics(students, subject):
    """Возвращает статистику по предмету"""
    all_grades = []
    student_count = 0
    
    for student in students:
        if "subjects" in student and subject in student["subjects"]:
            all_grades.extend(student["subjects"][subject])
            student_count += 1
    
    if not all_grades:
        return None
    
    return {
        "subject": subject,
        "student_count": student_count,
        "total_grades": len(all_grades),
        "average_grade": sum(all_grades) / len(all_grades),
        "min_grade": min(all_grades),
        "max_grade": max(all_grades)
    }

# Пример использования
stats = subject_statistics(students, "Математика")
if stats:
    print(f"Статистика по {stats['subject']}:")
    print(f"Количество студентов: {stats['student_count']}")
    print(f"Средний балл: {stats['average_grade']:.2f}")
```

---

### Задание 5: Создание классов для лучшей структуры

Преобразуйте программу, используя классы для лучшей организации кода:

```python
class Student:
    """Класс для представления студента"""
    def __init__(self, name, age, major):
        self.name = name
        self.age = age
        self.major = major
        self.subjects = {}
        self.enrollment_date = datetime.now().strftime("%Y-%m-%d")
    
    def add_grade(self, subject, grade):
        """Добавляет оценку по предмету"""
        if subject not in self.subjects:
            self.subjects[subject] = []
        self.subjects[subject].append(grade)
    
    def get_average_grade(self):
        """Вычисляет средний балл"""
        if not self.subjects:
            return 0
        
        all_grades = []
        for grades in self.subjects.values():
            all_grades.extend(grades)
        
        return sum(all_grades) / len(all_grades) if all_grades else 0
    
    def get_subject_grades(self, subject):
        """Возвращает оценки по предмету"""
        return self.subjects.get(subject, [])
    
    def __str__(self):
        return f"{self.name}, {self.age} лет, {self.major} (ср. балл: {self.get_average_grade():.2f})"

class StudentManager:
    """Класс для управления студентами"""
    def __init__(self, data_file="students_data.json"):
        self.students = []
        self.data_file = data_file
        self.load_data()
    
    def add_student(self, name, age, major):
        """Добавляет нового студента"""
        student = Student(name, age, major)
        self.students.append(student)
        return student
    
    def find_student(self, name):
        """Находит студента по имени"""
        for student in self.students:
            if student.name.lower() == name.lower():
                return student
        return None
    
    def remove_student(self, name):
        """Удаляет студента по имени"""
        for i, student in enumerate(self.students):
            if student.name.lower() == name.lower():
                del self.students[i]
                return True
        return False
    
    def get_students_by_major(self, major):
        """Возвращает студентов по специальности"""
        return [s for s in self.students if s.major.lower() == major.lower()]
    
    def get_high_performers(self, threshold=4.0):
        """Возвращает студентов с высоким средним баллом"""
        return [s for s in self.students if s.get_average_grade() >= threshold]
    
    def get_top_students(self, n=5):
        """Возвращает топ N студентов по среднему баллу"""
        sorted_students = sorted(self.students, key=lambda s: s.get_average_grade(), reverse=True)
        return sorted_students[:n]
    
    def save_data(self):
        """Сохраняет данные в файл"""
        try:
            data = []
            for student in self.students:
                student_data = {
                    "name": student.name,
                    "age": student.age,
                    "major": student.major,
                    "subjects": student.subjects,
                    "enrollment_date": student.enrollment_date
                }
                data.append(student_data)
            
            with open(self.data_file, 'w', encoding='utf-8') as f:
                json.dump(data, f, ensure_ascii=False, indent=2)
            return True
        except Exception as e:
            print(f"Ошибка при сохранении: {e}")
            return False
    
    def load_data(self):
        """Загружает данные из файла"""
        try:
            with open(self.data_file, 'r', encoding='utf-8') as f:
                data = json.load(f)
            
            self.students = []
            for student_data in data:
                student = Student(student_data["name"], student_data["age"], student_data["major"])
                student.subjects = student_data["subjects"]
                student.enrollment_date = student_data["enrollment_date"]
                self.students.append(student)
            return True
        except FileNotFoundError:
            return True  # Файл не существует, начинаем с пустого списка
        except Exception as e:
            print(f"Ошибка при загрузке: {e}")
            return False

# Использование классов в основной программе
manager = StudentManager()

while True:
    print("\n=== Система учета студентов (на основе классов) ===")
    print("1. Добавить студента")
    print("2. Добавить оценку")
    print("3. Просмотреть всех студентов")
    print("4. Найти студента")
    print("5. Удалить студента")
    print("6. Студенты с высоким баллом")
    print("7. Топ студентов")
    print("8. Студенты по специальности")
    print("0. Выход")
    
    choice = input("Выберите действие: ")
    
    if choice == "1":
        name = input("Введите имя студента: ")
        try:
            age = int(input("Введите возраст: "))
            major = input("Введите специальность: ")
            manager.add_student(name, age, major)
            print("Студент добавлен")
        except ValueError:
            print("Некорректный возраст")
    
    elif choice == "2":
        name = input("Введите имя студента: ")
        student = manager.find_student(name)
        if student:
            subject = input("Введите предмет: ")
            try:
                grade = float(input("Введите оценку: "))
                if 0 <= grade <= 10:
                    student.add_grade(subject, grade)
                    print("Оценка добавлена")
                else:
                    print("Оценка должна быть от 0 до 10")
            except ValueError:
                print("Некорректная оценка")
        else:
            print("Студент не найден")
    
    elif choice == "3":
        for i, student in enumerate(manager.students, 1):
            print(f"{i}. {student}")
    
    elif choice == "4":
        name = input("Введите имя для поиска: ")
        student = manager.find_student(name)
        if student:
            print(student)
            print("Предметы и оценки:")
            for subject, grades in student.subjects.items():
                avg = sum(grades) / len(grades) if grades else 0
                print(f"  {subject}: {grades} (ср. {avg:.2f})")
        else:
            print("Студент не найден")
    
    elif choice == "5":
        name = input("Введите имя студента для удаления: ")
        if manager.remove_student(name):
            print("Студент удален")
        else:
            print("Студент не найден")
    
    elif choice == "6":
        high_performers = manager.get_high_performers()
        print("Студенты с высоким баллом:")
        for student in high_performers:
            print(f"  {student}")
    
    elif choice == "7":
        top_students = manager.get_top_students(5)
        print("Топ 5 студентов:")
        for i, student in enumerate(top_students, 1):
            print(f"{i}. {student}")
    
    elif choice == "8":
        major = input("Введите специальность: ")
        students_by_major = manager.get_students_by_major(major)
        print(f"Студенты на специальности {major}:")
        for student in students_by_major:
            print(f"  {student}")
    
    elif choice == "0":
        manager.save_data()
        print("Данные сохранены. До свидания!")
        break
    
    else:
        print("Неверный выбор")
```

---

## Контрольные вопросы

1. Какие структуры данных использовались в программе и для чего?
2. В чем преимущества использования функций при разработке программы?
3. Как обрабатываются ошибки ввода данных?
4. Как реализована сохранение и загрузка данных?
5. В чем преимущества использования классов по сравнению с функциями?
6. Как организована структура программы?
7. Какие проверки данных реализованы?
8. Как реализована фильтрация и сортировка данных?

## Вывод

В ходе выполнения этой практической работы была создана комплексная программа учета студентов, включающая в себя:
- Работу с различными типами данных (списки, словари, строки, числа)
- Использование функций для структурирования кода
- Применение условных операторов и циклов
- Обработку исключений для повышения надежности
- Файловый ввод-вывод для сохранения данных
- Использование классов для лучшей организации кода

Программа демонстрирует интеграцию различных концепций программирования и показывает, как они могут работать вместе для решения реальной задачи. Такой подход позволяет создавать более сложные и функциональные приложения.
