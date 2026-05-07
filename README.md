# claude-skills

Маркетплейс [Claude Code](https://docs.claude.com/en/docs/claude-code) скилов от [@rukru](https://github.com/rukru).

## Доступные плагины

| Плагин | Версия | Описание |
|---|---|---|
| [`data-analysis`](plugins/data-analysis) | 1.0.0 | Протокол анализа данных (CSV/Excel): профилирование → аномалии → паттерны → executive summary с обязательными PNG-графиками |

## Что внутри `data-analysis`

Скил, который превращает ad-hoc «посмотри на этот csv» в воспроизводимый процесс:

1. **Профилирование** — размер, типы, пропуски, уникальные значения
2. **Поиск аномалий** ДО гипотез — выбросы, временные скачки, логические противоречия, дубликаты
3. **Описательная статистика** — распределения, разрезы по сегментам
4. **Поиск паттернов** — когорты, корреляции, Simpson's Paradox
5. **Executive Summary** — 3 вывода + 1 неочевидный инсайт + рекомендация + вопрос

На выходе — папка с `report.md` (markdown с YAML frontmatter), обязательными PNG-графиками (R1_, R2_…) и автономным `analysis.py` (pandas + matplotlib + seaborn).

## Prerequisites

- [Claude Code](https://docs.claude.com/en/docs/claude-code) (CLI / desktop / IDE-extension) — последняя версия с поддержкой `/plugin`
- Git и `gh` CLI (для marketplace из публичного GitHub-репо)
- Python 3.9+ с `pandas`, `matplotlib`, `seaborn` — для реальной работы скила (генерация графиков)

## Установка

В сессии Claude Code последовательно:

```text
/plugin marketplace add rukru/claude-skills
```
Ожидаемый ответ: `Added marketplace 'rukru-claude-skills'`.

```text
/plugin install data-analysis@rukru-claude-skills
```
Ожидаемый ответ: `Installed data-analysis@1.0.0`.

Проверить, что плагин подхватился:

```text
/plugin
```
В списке должен появиться `data-analysis` с пометкой `enabled`.

## Использование

После установки скил триггерится **автоматически** по описанию задачи. Примеры фраз, которые активируют его:

- «у меня csv с продажами за квартал, проанализируй»
- «загрузил excel с когортами, найди паттерны»
- «посмотри на этот датасет, есть ли аномалии?»
- «сделай профайлинг данных и отчёт с графиками»

Claude автоматически прогонит протокол из 5 шагов, оформит результат в нужный markdown с графиками и положит в папку анализа.

## Обновление

Когда мейнтейнер бампит версию плагина:

```text
/plugin marketplace update rukru-claude-skills
```

Новая версия подхватится при следующем запуске Claude Code (или сразу после `/reload-plugins`, если поддерживается).

## Удаление

```text
/plugin uninstall data-analysis@rukru-claude-skills
/plugin marketplace remove rukru-claude-skills
```

## Troubleshooting

**`/plugin` команда не найдена** — обнови Claude Code до последней версии: `claude update` (CLI) или через настройки IDE/desktop-приложения.

**`marketplace add` ругается на 404** — проверь имя репо и видимость (репо должен быть public, либо ставить через SSH с настроенным ключом для приватного).

**Скил не триггерится автоматически** — попробуй вызвать вручную через Skill-tool в Claude Code или явно сослаться на него: «используй data-analysis скил для анализа этого csv».

**Графики не генерируются** — установи зависимости: `pip install pandas matplotlib seaborn`.

## Структура репо

```
claude-skills/
├── .claude-plugin/
│   └── marketplace.json          # манифест маркетплейса
├── plugins/
│   └── data-analysis/
│       ├── .claude-plugin/
│       │   └── plugin.json       # манифест плагина
│       ├── skills/
│       │   └── data-analysis/
│       │       └── SKILL.md      # сам скил
│       └── README.md             # описание плагина
├── README.md
└── LICENSE
```

## Контрибьют

Pull requests welcome. Для добавления нового плагина:

1. Создайте `plugins/<plugin-name>/` со структурой плагина (`.claude-plugin/plugin.json` + `skills/`/`commands/`/`agents/`/`hooks/`)
2. Добавьте запись в `.claude-plugin/marketplace.json`
3. Бампните `version` существующих плагинов, если меняете их поведение
4. Откройте PR

## Лицензия

[MIT](LICENSE) © 2026 Timofey Novikov
