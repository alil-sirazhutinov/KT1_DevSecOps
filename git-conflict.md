# Merge-конфликт и его разрешение

## Причина

В `project-notes.md` одна строка изменена независимо в двух ветках.
Общая исходная версия: `- Порог предупреждения: 5 дней.`

- `main`, коммит `1764553`: `- Порог предупреждения: 3 дня.`
- `feature/expiry-policy`, коммит `933c3fa`: `- Порог предупреждения: 7 дней.`

При `git merge --no-ff feature/expiry-policy` Git остановил слияние:

```text
Auto-merging project-notes.md
CONFLICT (content): Merge conflict in project-notes.md
Automatic merge failed; fix conflicts and then commit the result.
```

В `git status --short` файл имел статус `UU`.

## Конфликтный фрагмент

```text
<<<<<<< HEAD
- Порог предупреждения: 3 дня.
=======
- Порог предупреждения: 7 дней.
>>>>>>> feature/expiry-policy
```

## Ручное разрешение

Конфликтный блок заменён согласованным правилом, маркеры удалены:

```text
- Порог предупреждения: настраивается от 1 до 30 дней, по умолчанию 3 дня.
```

Это сохраняет короткое предупреждение по умолчанию и позволяет выбрать неделю.
Затем выполнены:

```bash
git add project-notes.md expiry-examples.md
git commit -m "fix: resolve warning threshold conflict with configurable default"
```

Коммит исправления: [`d190a4f`](https://github.com/alil-sirazhutinov/KT1_DevSecOps/commit/d190a4f).
Это merge-коммит с двумя родителями: `1764553` и `933c3fa`.

## Проверка без изменения рабочих файлов

```bash
git show --no-patch --format=fuller d190a4f
git merge-tree --write-tree 1764553 933c3fa
git show d190a4f:project-notes.md
```

Для `merge-tree` ожидается код 1 и сообщение о конфликте.
Команда вычисляет слияние исходных версий, не меняя текущую ветку и рабочие файлы.
