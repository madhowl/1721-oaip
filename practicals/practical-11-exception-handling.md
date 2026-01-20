# Практическая работа 11: Обработка исключений

## Цель работы

Научиться использовать механизмы обработки исключений в Python, освоить конструкцию try-except-finally-else, научиться генерировать собственные исключения и правильно использовать обработку ошибок для создания надежных программ.

## Теоретическая часть

Исключение (exception) - это сигнал о том, что во время выполнения программы произошла ошибка. Когда Python сталкивается с ошибкой, он генерирует исключение, которое может быть перехвачено и обработано кодом программы. Обработка исключений позволяет программе корректно реагировать на ошибки и продолжать работу вместо аварийного завершения.

```python
# Пример обработки исключения
try:
    result = 10 / 0
except ZeroDivisionError:
    print("Ошибка: деление на ноль")
```

### Базовая структура обработки исключений:
```python
try:
    # код, который может вызвать исключение
    pass
except SpecificException:
    # код обработки конкретного исключения
    pass
except AnotherException as e:
    # код обработки другого исключения с доступом к объекту исключения
    pass
else:
    # код, который выполняется, если исключения не произошло
    pass
finally:
    # код, который выполняется в любом случае
    pass
```

## Практические задания

### Задание 1: Простая обработка исключения

Создайте программу, которая запрашивает у пользователя два числа и делит первое на второе. Обработайте исключение, которое возникает при делении на ноль.

**Пример выполнения:**
```
Введите первое число: 10
Введите второе число: 0
Ошибка: деление на ноль!
```

**Код для выполнения:**
```python
try:
    num1 = float(input("Введите первое число: "))
    num2 = float(input("Введите второе число: "))
    
    result = num1 / num2
    print(f"Результат: {num1} / {num2} = {result}")
except ZeroDivisionError:
    print("Ошибка: деление на ноль!")
except ValueError:
    print("Ошибка: введите числовое значение")
```

---

### Задание 2: Обработка нескольких типов исключений

Создайте программу, которая запрашивает у пользователя индекс для доступа к элементу списка. Обработайте исключения, которые могут возникнуть при неправильном индексе или неправильном формате ввода.

**Пример выполнения:**
```
Введите индекс: abc
Ошибка: введите целое число
```
или
```
Введите индекс: 10
Ошибка: индекс за пределами списка
```

**Код для выполнения:**
```python
my_list = [10, 20, 30, 40, 50]

try:
    index = int(input("Введите индекс: "))
    element = my_list[index]
    print(f"Элемент по индексу {index}: {element}")
except ValueError:
    print("Ошибка: введите целое число")
except IndexError:
    print("Ошибка: индекс за пределами списка")
except Exception as e:
    print(f"Неизвестная ошибка: {e}")
```

---

### Задание 3: Блоки else и finally

Модифицируйте предыдущую программу, добавив блоки `else` и `finally`.

**Код для выполнения:**
```python
my_list = [10, 20, 30, 40, 50]

try:
    index = int(input("Введите индекс: "))
    element = my_list[index]
except ValueError:
    print("Ошибка: введите целое число")
except IndexError:
    print("Ошибка: индекс за пределами списка")
else:
    # Этот блок выполнится, если исключения не произошло
    print(f"Элемент по индексу {index}: {element}")
    print("Операция выполнена успешно")
finally:
    # Этот блок выполнится в любом случае
    print("Завершение операции доступа к списку")
```

---

### Задание 4: Обработка исключений при работе с файлами

Создайте программу, которая пытается открыть файл для чтения и обрабатывает возможные исключения.

**Код для выполнения:**
```python
filename = input("Введите имя файла для чтения: ")

try:
    with open(filename, 'r', encoding='utf-8') as file:
        content = file.read()
        print("Содержимое файла:")
        print(content)
except FileNotFoundError:
    print(f"Ошибка: файл '{filename}' не найден")
except PermissionError:
    print(f"Ошибка: нет доступа к файлу '{filename}'")
except UnicodeDecodeError:
    print(f"Ошибка: не удалось декодировать файл '{filename}'. Возможно, проблема с кодировкой.")
except Exception as e:
    print(f"Произошла непредвиденная ошибка: {e}")
```

---

### Задание 5: Генерация исключений

Создайте функцию, которая проверяет, является ли число положительным. Если число отрицательное, генерируйте исключение `ValueError`.

**Пример выполнения:**
```
Введите число: -5
Ошибка: Число должно быть положительным
```

**Код для выполнения:**
```python
def check_positive(number):
    """Проверяет, является ли число положительным"""
    if number < 0:
        raise ValueError("Число должно быть положительным")
    return number

try:
    user_input = float(input("Введите число: "))
    result = check_positive(user_input)
    print(f"Число {result} положительное")
except ValueError as e:
    print(f"Ошибка: {e}")
except Exception as e:
    print(f"Неизвестная ошибка: {e}")
```

---

### Задание 6: Собственные классы исключений

Создайте собственный класс исключения для проверки корректности ввода пароля.

**Код для выполнения:**
```python
class WeakPasswordError(Exception):
    """Исключение для слабого пароля"""
    pass

class PasswordTooShortError(WeakPasswordError):
    """Исключение для слишком короткого пароля"""
    pass

class PasswordMissingDigitError(WeakPasswordError):
    """Исключение для пароля без цифр"""
    pass

def validate_password(password):
    """Проверяет надежность пароля"""
    if len(password) < 8:
        raise PasswordTooShortError("Пароль должен содержать не менее 8 символов")
    
    has_digit = any(char.isdigit() for char in password)
    if not has_digit:
        raise PasswordMissingDigitError("Пароль должен содержать хотя бы одну цифру")
    
    return True

# Пример использования
try:
    user_password = input("Введите пароль: ")
    validate_password(user_password)
    print("Пароль надежный")
except PasswordTooShortError as e:
    print(f"Ошибка: {e}")
except PasswordMissingDigitError as e:
    print(f"Ошибка: {e}")
except WeakPasswordError as e:
    print(f"Ошибка: {e}")
except Exception as e:
    print(f"Неизвестная ошибка: {e}")
```

---

### Задание 7: Обработка исключений в цикле

Создайте программу, которая запрашивает у пользователя числа до тех пор, пока он не введет корректное число.

**Пример выполнения:**
```
Введите число: abc
Некорректный ввод. Попробуйте снова.
Введите число: -5
Некорректный ввод. Попробуйте снова.
Введите число: 42
Вы ввели число: 42.0
```

**Код для выполнения:**
```python
def get_number():
    """Запрашивает у пользователя число до получения корректного ввода"""
    while True:
        try:
            user_input = input("Введите число: ")
            number = float(user_input)
            return number
        except ValueError:
            print("Некорректный ввод. Попробуйте снова.")
        except KeyboardInterrupt:
            print("\nПрограмма прервана пользователем")
            return None

result = get_number()
if result is not None:
    print(f"Вы ввели число: {result}")
```

---

### Задание 8: Обработка исключений в функциях

Создайте функцию безопасного деления, которая обрабатывает возможные исключения и возвращает результат или None в случае ошибки.

**Код для выполнения:**
```python
def safe_divide(a, b):
    """Безопасное деление с обработкой исключений"""
    try:
        result = a / b
        return result
    except ZeroDivisionError:
        print("Ошибка: деление на ноль")
        return None
    except TypeError:
        print("Ошибка: неподдерживаемые типы операндов")
        return None

# Примеры использования
print(safe_divide(10, 2))    # 5.0
print(safe_divide(10, 0))    # Ошибка: деление на ноль, None
print(safe_divide(10, "a"))  # Ошибка: неподдерживаемые типы операндов, None
```

---

### Задание 9: Контекстный менеджер с обработкой исключений

Создайте простой контекстный менеджер, который измеряет время выполнения блока кода и обрабатывает исключения.

**Код для выполнения:**
```python
import time

class Timer:
    """Контекстный менеджер для измерения времени выполнения"""
    
    def __enter__(self):
        self.start_time = time.time()
        return self
    
    def __exit__(self, exc_type, exc_value, traceback):
        end_time = time.time()
        elapsed_time = end_time - self.start_time
        print(f"Время выполнения: {elapsed_time:.2f} секунд")
        
        # Если было исключение, выводим информацию о нем
        if exc_type:
            print(f"Произошло исключение: {exc_type.__name__}: {exc_value}")
        
        # Возвращаем False, чтобы исключение продолжило распространение
        return False

# Пример использования
try:
    with Timer():
        time.sleep(1)  # Имитация работы
        print("Выполняемая операция")
        # raise ValueError("Тестовое исключение")  # Можно раскомментировать для тестирования
except ValueError as e:
    print(f"Поймано исключение: {e}")
```

---

### Задание 10: Обработка исключений при работе с JSON

Создайте программу, которая безопасно парсит JSON строку и обрабатывает возможные ошибки.

**Код для выполнения:**
```python
import json

def safe_parse_json(json_string):
    """Безопасный парсинг JSON строки"""
    try:
        data = json.loads(json_string)
        return data, None
    except json.JSONDecodeError as e:
        return None, f"Ошибка парсинга JSON: {e}"
    except Exception as e:
        return None, f"Неизвестная ошибка: {e}"

# Примеры использования
valid_json = '{"name": "Иван", "age": 30}'
invalid_json = '{"name": "Иван", "age":}'

data, error = safe_parse_json(valid_json)
if error:
    print(error)
else:
    print(f"Данные: {data}")

data, error = safe_parse_json(invalid_json)
if error:
    print(error)
else:
    print(f"Данные: {data}")
```

---

### Задание 11: Обработка исключений в работе со списками

Создайте программу, которая безопасно работает с операциями над списками.

**Код для выполнения:**
```python
def safe_list_operations():
    """Демонстрирует безопасную работу со списками"""
    my_list = [1, 2, 3, 4, 5]
    
    while True:
        print("\n1. Доступ к элементу по индексу")
        print("2. Добавить элемент")
        print("3. Удалить элемент")
        print("4. Выйти")
        
        try:
            choice = int(input("Выберите действие: "))
        except ValueError:
            print("Ошибка: введите число")
            continue
        
        try:
            if choice == 1:
                index = int(input("Введите индекс: "))
                print(f"Элемент по индексу {index}: {my_list[index]}")
            elif choice == 2:
                element = input("Введите элемент для добавления: ")
                # Пытаемся преобразовать к числу, если возможно
                try:
                    element = int(element)
                except ValueError:
                    try:
                        element = float(element)
                    except ValueError:
                        pass  # Оставляем как строку
                my_list.append(element)
                print(f"Элемент добавлен. Текущий список: {my_list}")
            elif choice == 3:
                index = int(input("Введите индекс для удаления: "))
                removed = my_list.pop(index)
                print(f"Элемент {removed} удален. Текущий список: {my_list}")
            elif choice == 4:
                break
            else:
                print("Неверный выбор")
        except IndexError:
            print("Ошибка: индекс за пределами списка")
        except ValueError as e:
            print(f"Ошибка значения: {e}")
        except Exception as e:
            print(f"Произошла ошибка: {e}")

# Запуск программы
safe_list_operations()
```

---

### Задание 12: Использование оператора assert

Используйте оператор `assert` для проверки условий в коде и генерации `AssertionError` при их несоблюдении.

**Код для выполнения:**
```python
def calculate_average(numbers):
    """Вычисляет среднее значение списка чисел"""
    assert len(numbers) > 0, "Список чисел не должен быть пустым"
    assert all(isinstance(x, (int, float)) for x in numbers), "Все элементы должны быть числами"
    
    return sum(numbers) / len(numbers)

# Примеры использования
try:
    print(calculate_average([1, 2, 3, 4, 5]))  # 3.0
    print(calculate_average([]))  # AssertionError: Список чисел не должен быть пустым
except AssertionError as e:
    print(f"Ошибка утверждения: {e}")

try:
    print(calculate_average([1, 2, "3", 4]))  # AssertionError: Все элементы должны быть числами
except AssertionError as e:
    print(f"Ошибка утверждения: {e}")
```

---

### Задание 13: Комплексная задача - калькулятор с обработкой исключений

Создайте программу калькулятора, которая обрабатывает все возможные исключения при выполнении операций.

**Код для выполнения:**
```python
def calculator():
    """Калькулятор с обработкой исключений"""
    print("Калькулятор. Поддерживаемые операции: +, -, *, /")
    print("Для выхода введите 'quit'")
    
    while True:
        try:
            # Ввод первого числа
            first_input = input("\nВведите первое число (или 'quit' для выхода): ")
            if first_input.lower() == 'quit':
                break
            
            num1 = float(first_input)
            
            # Ввод операции
            operation = input("Введите операцию (+, -, *, /): ")
            if operation not in ['+', '-', '*', '/']:
                raise ValueError(f"Неподдерживаемая операция: {operation}")
            
            # Ввод второго числа
            second_input = input("Введите второе число: ")
            num2 = float(second_input)
            
            # Выполнение операции
            if operation == '+':
                result = num1 + num2
            elif operation == '-':
                result = num1 - num2
            elif operation == '*':
                result = num1 * num2
            elif operation == '/':
                if num2 == 0:
                    raise ZeroDivisionError("деление на ноль")
                result = num1 / num2
            
            print(f"Результат: {num1} {operation} {num2} = {result}")
            
        except ValueError as e:
            if "could not convert" in str(e):
                print("Ошибка: введите числовое значение")
            else:
                print(f"Ошибка: {e}")
        except ZeroDivisionError as e:
            print(f"Ошибка: {e}")
        except KeyboardInterrupt:
            print("\nПрограмма прервана пользователем")
            break
        except Exception as e:
            print(f"Непредвиденная ошибка: {e}")

# Запуск калькулятора
calculator()
```

---

### Задание 14: Обработка исключений при работе с API (имитация)

Создайте программу, которая имитирует работу с API и обрабатывает возможные ошибки.

**Код для выполнения:**
```python
import random
import time

def simulate_api_call(endpoint):
    """Имитация вызова API с возможными ошибками"""
    # Имитация задержки
    time.sleep(0.5)
    
    # Случайно генерируем результат
    rand_num = random.random()
    
    if rand_num < 0.1:  # 10% шанс ошибки соединения
        raise ConnectionError("Не удалось подключиться к серверу")
    elif rand_num < 0.2:  # 10% шанс таймаута
        raise TimeoutError("Время ожидания истекло")
    elif rand_num < 0.3:  # 10% шанс ошибки сервера
        raise RuntimeError("Ошибка сервера")
    elif rand_num < 0.4:  # 10% шанс ошибки данных
        raise ValueError("Некорректные данные")
    else:
        # Успешный результат
        return {"status": "success", "data": f"Данные с эндпоинта {endpoint}"}

def api_client():
    """Клиент для работы с API"""
    endpoints = ["/users", "/posts", "/comments", "/albums"]
    
    for endpoint in endpoints:
        try:
            print(f"Запрос к {endpoint}...")
            result = simulate_api_call(endpoint)
            print(f"Успешно: {result}")
        except ConnectionError as e:
            print(f"Ошибка подключения: {e}")
        except TimeoutError as e:
            print(f"Таймаут: {e}")
        except ValueError as e:
            print(f"Ошибка данных: {e}")
        except RuntimeError as e:
            print(f"Серверная ошибка: {e}")
        except Exception as e:
            print(f"Неизвестная ошибка: {e}")
        finally:
            print("---")

# Запуск клиента
api_client()
```

---

### Задание 15: Обработка исключений в банковской системе

Создайте простую банковскую систему с обработкой исключений для различных операций.

**Код для выполнения:**
```python
class InsufficientFundsError(Exception):
    """Исключение для недостатка средств"""
    pass

class AccountFrozenError(Exception):
    """Исключение для замороженного счета"""
    pass

class BankAccount:
    """Класс банковского счета"""
    
    def __init__(self, account_number, initial_balance=0):
        self.account_number = account_number
        self.balance = initial_balance
        self.is_frozen = False
    
    def deposit(self, amount):
        """Пополнение счета"""
        if self.is_frozen:
            raise AccountFrozenError("Счет заморожен")
        
        if amount <= 0:
            raise ValueError("Сумма пополнения должна быть положительной")
        
        self.balance += amount
        return self.balance
    
    def withdraw(self, amount):
        """Снятие со счета"""
        if self.is_frozen:
            raise AccountFrozenError("Счет заморожен")
        
        if amount <= 0:
            raise ValueError("Сумма снятия должна быть положительной")
        
        if amount > self.balance:
            raise InsufficientFundsError("Недостаточно средств на счете")
        
        self.balance -= amount
        return self.balance
    
    def get_balance(self):
        """Получение баланса"""
        if self.is_frozen:
            raise AccountFrozenError("Счет заморожен")
        return self.balance

def banking_system():
    """Система банковских операций"""
    account = BankAccount("ACC001", 1000)
    
    print("Банковская система")
    print(f"Счет: {account.account_number}, Баланс: {account.balance}")
    
    operations = [
        (lambda: account.deposit(500), "Пополнение на 500"),
        (lambda: account.withdraw(200), "Снятие 200"),
        (lambda: account.withdraw(2000), "Снятие 2000 (ошибка)"),
        (lambda: setattr(account, 'is_frozen', True) or print("Счет заморожен")),
        (lambda: account.deposit(100), "Пополнение (ошибка - счет заморожен)"),
        (lambda: account.get_balance(), "Получение баланса (ошибка - счет заморожен)")
    ]
    
    for operation, description in operations:
        try:
            result = operation()
            if result is not None:
                print(f"{description}: Успех, баланс = {result}")
            else:
                print(f"{description}: Выполнено")
        except InsufficientFundsError as e:
            print(f"{description}: Ошибка - {e}")
        except AccountFrozenError as e:
            print(f"{description}: Ошибка - {e}")
        except ValueError as e:
            print(f"{description}: Ошибка - {e}")
        except Exception as e:
            print(f"{description}: Неизвестная ошибка - {e}")

# Запуск банковской системы
banking_system()
```

---

## Контрольные вопросы

1. Что такое исключение в Python?
2. Какой синтаксис используется для обработки исключений?
3. В чем разница между блоками except, else и finally?
4. Какие стандартные исключения вы знаете?
5. Как создать собственный класс исключения?
6. Для чего используется инструкция raise?
7. Как обработать несколько типов исключений?
8. Что такое контекстный менеджер и как он связан с обработкой исключений?
9. В чем преимущество обработки исключений перед проверкой условий?
10. Что делает оператор assert и в каких случаях его использовать?

## Вывод

В ходе этой практической работы были освоены основы обработки исключений в Python. Были рассмотрены различные типы исключений, способы их перехвата и обработки, создание собственных классов исключений, а также применение обработки исключений в различных ситуациях. Правильная обработка исключений позволяет создавать более надежные и устойчивые к ошибкам программы, обеспечивая корректную работу даже в случае возникновения непредвиденных ситуаций.
