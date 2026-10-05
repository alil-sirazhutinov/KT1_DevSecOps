# План REST API

Базовый путь: `/api/v1`.

| Метод | Маршрут | Назначение |
|---|---|---|
| POST | `/products` | Добавить продукт |
| GET | `/products` | Активные запасы |
| GET | `/products?status=expiring` | Продукты с близким сроком годности |
| GET | `/products?status=expired` | Просроченные продукты |
| PATCH | `/products/:id` | Изменить данные или статус |
| GET | `/categories` | Справочник категорий |
| GET | `/settings` | Настройки предупреждения |
| PATCH | `/settings` | Изменить порог предупреждения |

## Пример добавления

```json
{
  "name": "Молоко",
  "category": "dairy",
  "quantity": 1,
  "unit": "l",
  "storage": "fridge",
  "purchasedOn": "2026-10-05",
  "expiresOn": "2026-10-08"
}
```

Успешное создание: HTTP 201, объект продукта с `id` и статусом `active`.
Статус хранения: `active`, `consumed`, `discarded`.
`expiring` и `expired` — вычисляемые фильтры для активных продуктов.

## Валидация

- `name`: непустая строка, до 100 символов после trim.
- `quantity`: число > 0; для `pcs` — целое.
- `category`, `storage`, `unit`: значения из справочника `categories.md`.
- `purchasedOn`, `expiresOn`: существующие даты YYYY-MM-DD;
  дата годности не раньше даты покупки. Просроченный продукт можно внести для учёта.
- `status`: `active`, `consumed` или `discarded`.
- `warningDays`: целое от 1 до 30, по умолчанию 3.

Ошибки: HTTP 400 `{ "error": "validation_error", "field": "quantity" }`,
HTTP 404 `{ "error": "not_found" }` для неизвестного id.
