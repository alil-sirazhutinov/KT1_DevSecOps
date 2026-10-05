# Памятка для защиты

## Рассказ

Тема — учёт сроков годности домашних продуктов. Она выбрана как понятная
предметная область для будущего сервиса с API, базой данных и контейнерами.
MVP позволит добавлять продукты, видеть близкие сроки годности и отмечать расход.

В начале добавлены README, заметки о сущностях и план API.
Затем в отдельных ветках подготовлены категории, примеры расчёта сроков
и правила валидации. Каждый коммит фиксирует отдельный осмысленный шаг.

Ветки: `main` — итоговые документы, `feature/categories` — справочник,
`feature/expiry-policy` — политика предупреждений и примеры,
`feature/validation` — проверка входных данных.
Все три рабочие ветки слиты в main и сохранены на GitHub.

Конфликт возник в строке порога предупреждения в project-notes.md:
main выбрал 3 дня, другая ветка — 7 дней. Маркеры конфликта заменены правилом
«настраивается от 1 до 30 дней, по умолчанию 3 дня».
Отдельный коммит исправления — d190a4f, у него два родителя.

На графе точки — коммиты, линии — связи с родителями.
Расхождение показывает независимую работу, соединение — слияние.
Граф подтверждает ветвление и merge, а конфликт подтверждается git-conflict.md
и повторным расчётом слияния исходных коммитов.

## Команды для демонстрации

```bash
git branch -a
git rev-list --count --all
git log --all --graph --oneline --decorate
git log --merges --oneline
git show --no-patch --format=fuller d190a4f
git merge-tree --write-tree 1764553 933c3fa
git show d190a4f:project-notes.md
```

Для merge-tree ожидаются код 1 и сообщение CONFLICT; рабочие файлы не меняются.
Нужна версия Git с поддержкой merge-tree --write-tree.

## Что показать

- [Репозиторий](https://github.com/alil-sirazhutinov/pantry-expiry-service).
- [Коммиты](https://github.com/alil-sirazhutinov/pantry-expiry-service/commits/main).
- [Ветки](https://github.com/alil-sirazhutinov/pantry-expiry-service/branches).
- [Граф Network](https://github.com/alil-sirazhutinov/pantry-expiry-service/network).
- Описание конфликта и коммит d190a4f.

Сдать ссылку на репозиторий в систему обучения.
