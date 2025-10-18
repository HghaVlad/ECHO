# Руководство по работе с репозиторием

## Общие принципы

Этот репозиторий использует **Git Flow-подход**, **чистую историю коммитов** и **обязательную систему code review (approve)**.  
Основные цели — прозрачность, единообразие и качество кода.

---

## Как внести изменения

1. **Создайте новую ветку** от `main` или `develop`:
   ```bash
   git checkout develop
   git pull
   git checkout -b feature/<short-description>
   ```

2. **Внесите изменения** в код, добавьте тесты (если применимо) и убедитесь, что проект успешно собирается.

3. **Проверьте кодстайл и линтеры**.

4. **Создайте коммит**, следуя правилам именования (см. ниже).

5. **Откройте Pull Request (PR)**:

   * Базовая ветка: `develop`
   * Название PR: совпадает с названием ветки
   * В описании: кратко укажите, что сделано

---

## Именование веток

Используем префиксы в зависимости от типа изменений:

| Тип ветки        | Префикс     | Пример                            |
| ---------------- | ----------- | --------------------------------- |
| Новая фича       | `feature/`  | `feature/add-login-form`          |
| Исправление      | `fix/`      | `fix/user-auth-bug`               |
| Рефакторинг      | `refactor/` | `refactor/improve-database-layer` |
| Документация     | `docs/`     | `docs/update-readme`              |
| Зависимости      | `chore/`    | `chore/update-dependencies`       |
| Релизная ветка   | `release/`  | `release/v1.2.0`                  |
| Хотфикс          | `hotfix/`   | `hotfix/critical-crash-fix`       |

---

## Стиль коммитов

Следуем соглашению **Conventional Commits**:

```
<type>(<scope>): <short summary>
```

### Примеры:

```
feat(auth): add JWT token validation
fix(api): correct null pointer in user endpoint
refactor(core): optimize data loading
docs(readme): update contribution guide
```

### Допустимые типы:

* `feat` — новая функциональность
* `fix` — исправление ошибки
* `refactor` — изменение структуры кода без изменения логики
* `docs` — документация
* `style` — форматирование, не влияющее на логику
* `test` — тесты
* `chore` — прочие изменения (скрипты, конфигурация и т.д.)

> Коммиты должны быть **атомарными** — один логический шаг = один коммит.

---

## Code Review и система Approve’ов

Каждый Pull Request должен пройти **code review** перед слиянием. Необходимо получить 3 апрува, от каждого разработчика, не являющегося автором изменений.

> Без нужного количества approve’ов PR не может быть замержен.

После получения всех необходимых approve’ов автор выполняет **squash merge** или **rebase merge**, чтобы сохранить чистую историю.

---

## Проверка перед слиянием

Перед merge в `develop` или `main` необходимо убедиться:

* ✅ Нет конфликтов с целевой веткой
* ✅ Коммиты чистые и осмысленные
* ✅ Есть approve’ы от требуемых ревьюеров

---

## Релизы

1. Для подготовки релиза создайте ветку:

   ```bash
   git checkout develop
   git checkout -b release/Final
   ```
2. Выполните merge в `main` и `develop`:

   ```bash
   git checkout main
   git merge release/Final
   git tag -a Final -m "Release Final version"
   git push --tags
   ```
---