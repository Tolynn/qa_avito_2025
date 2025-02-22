# ОТЧЕТЫ О БАГАХ

## BUG-001: Некорректное сохранение поля `name` при создании объявления

**Описание:**
При отправке `POST /api/1/item` API сохраняет некорректное значение в поле `name`.

**Шаги для воспроизведения:**
1. Выполнить `POST`-запрос на `https://qa-internship.avito.com/api/1/item` с телом:
   ```json
   {
       "name": "Товар",
       "price": 1000,
       "sellerId": 1111119,
       "statistics": {
           "contacts": 0,
           "likes": 0,
           "viewCount": 0
       }
   }
   ```
2. Получить ID созданного объявления из ответа.
3. Отправить `GET`-запрос `https://qa-internship.avito.com/api/1/item/{ID}`.
4. Проверить поле `name` в ответе.

**Ожидаемый результат:**
- Поле `name` совпадает с переданным значением (`"Товар"`).

**Фактический результат:**
- Поле `name` содержит некорректное значение (`"dsdsd"`).

**Приоритет:** Высокий
**Статус:** Открыт
**Среда:** QA-сервер `https://qa-internship.avito.com`

**Дополнительно:**
- Ошибка воспроизводится стабильно.
- Возможная причина: некорректная обработка входных данных на сервере.

---

## BUG-002: Отсутствует проверка на отрицательную цену при создании объявления

**Описание:**
При отправке `POST /api/1/item` с отрицательным значением в поле `price` API принимает запрос и создает объявление.

**Шаги для воспроизведения:**
1. Отправить `POST`-запрос на `https://qa-internship.avito.com/api/1/item` с телом:
   ```json
   {
       "name": "Товар",
       "price": -500,
       "sellerId": 1111119,
       "statistics": {
           "contacts": 0,
           "likes": 0,
           "viewCount": 0
       }
   }
   ```
2. Проверить ответ сервера.
3. Выполнить `GET`-запрос на `https://qa-internship.avito.com/api/1/item/{ID}`.

**Ожидаемый результат:**
- Сервер должен вернуть ошибку `400 Bad Request` с сообщением об ошибке.

**Фактический результат:**
- Объявление успешно создается с отрицательной ценой.

**Приоритет:** Средний
**Статус:** Открыт
**Среда:** QA-сервер `https://qa-internship.avito.com`

**Дополнительно:**
- Отсутствует серверная валидация для поля `price`.

---

## BUG-003: Ошибка при получении объявления по несуществующему ID

**Описание:**
При выполнении `GET /api/1/item/{ID}` с несуществующим `ID` сервер возвращает `400 Bad Request` вместо `404 Not Found`.

**Шаги для воспроизведения:**
1. Выполнить `GET`-запрос `https://qa-internship.avito.com/api/1/item/123456789`.

**Ожидаемый результат:**
- Сервер должен вернуть `404 Not Found` с сообщением `"item not found"`.

**Фактический результат:**
- Сервер возвращает `400 Bad Request` с сообщением `"Передан некорректный идентификатор объявления"`.

**Приоритет:** Средний
**Статус:** Открыт
**Среда:** QA-сервер `https://qa-internship.avito.com`

**Дополнительно:**
- Ошибка может быть связана с некорректной проверкой параметра `ID`.

