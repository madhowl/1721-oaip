# Лекция 11: Обработка исключений

## Введение

Обработка исключений - это важный механизм в Python, позволяющий программам корректно реагировать на ошибки и неожиданные ситуации. Исключения позволяют отделить нормальный ход выполнения программы от обработки ошибок, делая код более надежным и читаемым. В этой лекции мы подробно рассмотрим, как работать с исключениями в Python.

## Основное содержание

### Что такое исключения

**Исключение (exception)** - это сигнал о том, что во время выполнения программы возникла ошибка. Когда Python сталкивается с ошибкой, он генерирует исключение, которое может быть перехвачено и обработано кодом программы.

```python
# Пример генерации исключения
try:
    result = 10 / 0  # Деление на ноль
except ZeroDivisionError:
    print("Ошибка: деление на ноль!")
```

### Иерархия исключений

В Python все исключения являются классами, и они образуют иерархию. Основные классы исключений:

```
BaseException
 +-- SystemExit
 +-- KeyboardInterrupt
 +-- GeneratorExit
 +-- Exception
      +-- StopIteration
      +-- ArithmeticError
      |    +-- FloatingPointError
      |    +-- OverflowError
      |    +-- ZeroDivisionError
      +-- AttributeError
      +-- EOFError
      +-- ImportError
      |    +-- ModuleNotFoundError
      +-- LookupError
      |    +-- IndexError
      |    +-- KeyError
      +-- NameError
      +-- OSError
      |    +-- FileNotFoundError
      |    +-- PermissionError
      +-- RuntimeError
      +-- SyntaxError
      +-- TypeError
      +-- ValueError
```

### Конструкция try-except

Основная конструкция для обработки исключений:

```python
try:
    # Код, который может вызвать исключение
    risky_code()
except SpecificException:
    # Код для обработки конкретного исключения
    handle_error()
```

### Обработка разных типов исключений

```python
def safe_divide(a, b):
    try:
        result = a / b
        return result
    except ZeroDivisionError:
        print("Ошибка: деление на ноль!")
        return None
    except TypeError:
        print("Ошибка: неподходящий тип данных!")
        return None

# Примеры использования
print(safe_divide(10, 2))   # 5.0
print(safe_divide(10, 0))   # Ошибка: деление на ноль!
print(safe_divide("10", 2)) # Ошибка: неподходящий тип данных!
```

### Обработка нескольких исключений в одном блоке

```python
def process_data(data, index):
    try:
        # Несколько операций, которые могут вызвать разные исключения
        value = data[index]
        result = 100 / value
        return result
    except (IndexError, ZeroDivisionError) as e:
        print(f"Обработано исключение: {type(e).__name__}: {e}")
        return None

# Примеры
numbers = [10, 20, 0, 40]
print(process_data(numbers, 1))  # 5.0
print(process_data(numbers, 2))  # Обработано исключение: ZeroDivisionError: division by zero
print(process_data(numbers, 10)) # Обработано исключение: IndexError: list index out of range
```

### Блок else

Блок `else` выполняется, если в блоке `try` не было исключений:

```python
def read_file(filename):
    try:
        file = open(filename, 'r')
    except FileNotFoundError:
        print(f"Файл {filename} не найден")
        return None
    else:
        # Этот блок выполнится только если не было исключения
        content = file.read()
        file.close()
        print("Файл успешно прочитан")
        return content

# Примеры
content = read_file("existing_file.txt")
if content:
    print(content)
```

### Блок finally

Блок `finally` выполняется всегда, независимо от того, было ли исключение:

```python
def divide_with_cleanup(a, b):
    result = None
    try:
        result = a / b
        print(f"Результат: {result}")
    except ZeroDivisionError:
        print("Ошибка: деление на ноль!")
    finally:
        # Этот блок выполнится в любом случае
        print("Завершение операции деления")
        if result is not None:
            print(f"Финальный результат: {result}")
        else:
            print("Операция не завершена успешно")

# Примеры
divide_with_cleanup(10, 2)  # Результат: 5.0, Завершение операции деления, Финальный результат: 5.0
divide_with_cleanup(10, 0)  # Ошибка: деление на ноль!, Завершение операции деления, Операция не завершена успешно
```

### Генерация исключений

Исключения можно генерировать вручную с помощью ключевого слова `raise`:

```python
def validate_age(age):
    if age < 0:
        raise ValueError("Возраст не может быть отрицательным")
    if age > 150:
        raise ValueError("Возраст не может быть больше 150")
    return True

def calculate_discount(age):
    try:
        validate_age(age)
        if age >= 65:
            return 0.2  # 20% скидка для пенсионеров
        elif age <= 18:
            return 0.1  # 10% скидка для детей
        else:
            return 0.0  # Без скидки
    except ValueError as e:
        print(f"Ошибка валидации: {e}")
        return None

# Примеры
print(calculate_discount(25))   # 0.0
print(calculate_discount(-5))   # Ошибка валидации: Возраст не может быть отрицательным
print(calculate_discount(200))  # Ошибка валидации: Возраст не может быть больше 150
```

### Пользовательские исключения

Можно создавать свои классы исключений, наследуя их от базовых классов исключений:

```python
class InsufficientFundsError(Exception):
    """Исключение при недостатке средств"""
    def __init__(self, balance, amount):
        self.balance = balance
        self.amount = amount
        super().__init__(f"Недостаточно средств: баланс {balance}, запрошено {amount}")

class BankAccount:
    def __init__(self, initial_balance=0):
        self.balance = initial_balance
    
    def withdraw(self, amount):
        if amount > self.balance:
            raise InsufficientFundsError(self.balance, amount)
        self.balance -= amount
        return self.balance

# Использование пользовательского исключения
account = BankAccount(100)
try:
    account.withdraw(150)
except InsufficientFundsError as e:
    print(f"Ошибка: {e}")
    print(f"Баланс: {e.balance}, Запрошено: {e.amount}")
```

### Логирование исключений

Для отладки и мониторинга ошибок полезно логировать информацию об исключениях:

```python
import traceback
import logging

# Настройка логирования
logging.basicConfig(level=logging.INFO, format='%(asctime)s - %(levelname)s - %(message)s')

def risky_operation(x, y):
    try:
        result = x / y
        logging.info(f"Операция {x}/{y} выполнена успешно: {result}")
        return result
    except ZeroDivisionError:
        logging.error(f"Попытка деления {x} на ноль")
        # Полный трейсбек для отладки
        traceback.print_exc()
        return None
    except Exception as e:
        logging.error(f"Неожиданная ошибка: {type(e).__name__}: {e}")
        traceback.print_exc()
        return None

# Пример использования
risky_operation(10, 2)  # Успешно
risky_operation(10, 0)  # Ошибка деления на ноль
```

### Контекстные менеджеры и обработка исключений

Контекстные менеджеры (с использованием `with`) автоматически обрабатывают закрытие ресурсов:

```python
# Без контекстного менеджера
file = open("data.txt", "r")
try:
    content = file.read()
    # Обработка данных
finally:
    file.close()  # Важно закрыть файл в любом случае

# С контекстным менеджером (рекомендуемый способ)
try:
    with open("data.txt", "r") as file:
        content = file.read()
        # Обработка данных
except FileNotFoundError:
    print("Файл не найден")
except IOError:
    print("Ошибка ввода-вывода")
# Файл автоматически закрывается после выхода из блока with
```

### Практические рекомендации

1. **Уточняйте типы исключений** - ловите конкретные исключения, а не общее `Exception`
2. **Не игнорируйте исключения** - всегда обрабатывайте их должным образом
3. **Используйте finally или with** для очистки ресурсов
4. **Создавайте пользовательские исключения** для бизнес-логики
5. **Логируйте ошибки** для последующей диагностики

## Практические примеры

### Пример 1: Обработка ввода пользователя

```python
def get_integer_input(prompt, min_value=None, max_value=None):
    """Безопасное получение целого числа от пользователя"""
    while True:
        try:
            value = int(input(prompt))
            
            if min_value is not None and value < min_value:
                print(f"Значение должно быть не меньше {min_value}")
                continue
            
            if max_value is not None and value > max_value:
                print(f"Значение должно быть не больше {max_value}")
                continue
                
            return value
        except ValueError:
            print("Пожалуйста, введите целое число")
        except KeyboardInterrupt:
            print("\nОперация отменена пользователем")
            return None

# Пример использования
number = get_integer_input("Введите число от 1 до 100: ", 1, 100)
if number is not None:
    print(f"Вы ввели: {number}")
```

### Пример 2: Работа с файлами

```python
def read_config_file(filename):
    """Чтение конфигурационного файла"""
    config = {}
    
    try:
        with open(filename, 'r', encoding='utf-8') as file:
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
        print(f"Файл конфигурации {filename} не найден")
        return None
    except PermissionError:
        print(f"Нет доступа к файлу {filename}")
        return None
    except UnicodeDecodeError:
        print(f"Ошибка кодировки файла {filename}")
        return None
    except Exception as e:
        print(f"Неожиданная ошибка при чтении файла: {e}")
        return None
    
    return config

# Пример использования
config = read_config_file("config.txt")
if config:
    print("Конфигурация загружена:")
    for key, value in config.items():
        print(f"  {key} = {value}")
```

### Пример 3: Обработка API-запросов

```python
import requests
from typing import Optional, Dict, Any

def fetch_user_data(user_id: int) -> Optional[Dict[Any, Any]]:
    """Получение данных пользователя через API"""
    url = f"https://api.example.com/users/{user_id}"
    
    try:
        response = requests.get(url, timeout=10)
        
        # Проверяем статус ответа
        response.raise_for_status()  # Вызывает исключение для кодов 4xx и 5xx
        
        # Пытаемся распарсить JSON
        user_data = response.json()
        return user_data
        
    except requests.exceptions.ConnectionError:
        print("Ошибка подключения к API")
    except requests.exceptions.Timeout:
        print("Таймаут запроса")
    except requests.exceptions.HTTPError as e:
        print(f"HTTP ошибка: {e}")
        if response.status_code == 404:
            print("Пользователь не найден")
    except requests.exceptions.RequestException as e:
        print(f"Ошибка запроса: {e}")
    except ValueError:  # Ошибка при парсинге JSON
        print("Ответ сервера не является корректным JSON")
    except Exception as e:
        print(f"Неожиданная ошибка: {e}")
    
    return None

# Пример использования
user_data = fetch_user_data(123)
if user_data:
    print(f"Имя пользователя: {user_data.get('name')}")
```

## Заключение

В этой лекции мы подробно рассмотрели обработку исключений в Python:

1. **Конструкция try-except** для перехвата и обработки исключений
2. **Различные типы исключений** и их иерархия
3. **Дополнительные блоки** else и finally
4. **Генерация исключений** с помощью raise
5. **Пользовательские исключения** для специфических ситуаций
6. **Практические примеры** обработки исключений в реальных сценариях

Обработка исключений - важный инструмент для создания надежных программ, которые могут корректно реагировать на ошибки и неожиданные ситуации. В следующей лекции мы рассмотрим работу с файлами в Python.
