# Настройка GitHub Actions в репозитории

## CSpell

В данном репозитории используется **GitHub Action CSpell**, предназначенный для автоматической проверки орфографии во всех `.md`, `.txt` и `.json` файлах.  
Action помогает поддерживать качество документации, снижая количество опечаток и ошибок при оформлении анкет, протоколов и планов коммуникаций.

---

### Файлы конфигурации

- **`./.github/workflows/spell_checking.yml`** — основной workflow-файл, определяющий запуск проверки.  
- **`./cspell.json`** — файл настроек [Code Spell Checker (cspell)](https://github.com/streetsidesoftware/cspell) — словаря и исключений.  

---

### Пример workflow-файла

Файл: `.github/workflows/spell_checking.yml`

```yaml
name: 'Check spelling'
on:
  pull_request:
  workflow_dispatch:

jobs:
  spellcheck:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      
      - name: Install cspell and Russian dictionary
        run: |
          npm install cspell @cspell/dict-ru_ru
          
      - name: Run cspell
        run: |
          npx cspell "**/*.md" --config cspell.json --verbose --show-suggestions
```

---

### Пример cspell.json
```json
{
  "version": "0.2",
  "import": ["@cspell/dict-ru_ru/cspell-ext.json"],
  "language": "ru_ru,en,ru",
  "ignoreWords": ["кодстайл","фича","Релизная","Хотфикс","Коммиты","апрува","замержен","ревьюеров"]
}
```

---