# Инструкция по запуску тестов для проекта AvitoTech_QA-trainee


## Описание
Этот проект содержит автоматизированные тесты для API с использованием `pytest` и `requests`. Тесты проверяют основные операции с объявлениями: создание, получение, сравнение данных и обработку несуществующих объектов.

## Требования
- `Python 3.7+`
- `pytest`
- `requests`

## Установка
1. Клонируйте репозиторий:
   ```sh
   git clone https://github.com/Tolynn/qa_avito_2025.git
   cd test_api
   ```
2. Установите пакеты:
   ```sh
   pip install pytest requests
   ```

## Запуск тестов
Для запуска всех тестов выполните:
```sh
pytest -v
```


## Структура проекта
```
/
│── Task1.md # Задание 1
│── test_api.py  # Основные тесты API к Заданию 2.1
│── README.md  # Документация
│── TESTCASES.md  # Описание тест-кейсов
│── BUGS.md  # Баг-репорты
```


