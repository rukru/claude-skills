# claude-skills

Маркетплейс [Claude Code](https://docs.claude.com/en/docs/claude-code) скилов от [@rukru](https://github.com/rukru).

## Доступные плагины

| Плагин | Версия | Описание |
|---|---|---|
| [`data-analysis`](plugins/data-analysis) | 1.0.0 | Протокол анализа данных (CSV/Excel): профилирование → аномалии → паттерны → executive summary с обязательными PNG-графиками |

## Установка

В Claude Code выполните:

```
/plugin marketplace add rukru/claude-skills
/plugin install data-analysis@rukru-claude-skills
```

После установки скил триггерится автоматически по описанию задачи (например: «у меня csv с продажами, проанализируй»).

## Обновление

```
/plugin marketplace update rukru-claude-skills
```

Затем перезагрузите плагины (`/reload-plugins` или новой сессией Claude Code).

## Удаление

```
/plugin uninstall data-analysis@rukru-claude-skills
/plugin marketplace remove rukru-claude-skills
```

## Структура репо

```
claude-skills/
├── .claude-plugin/
│   └── marketplace.json          # манифест маркетплейса
├── plugins/
│   └── data-analysis/
│       ├── .claude-plugin/
│       │   └── plugin.json       # манифест плагина
│       └── skills/
│           └── data-analysis/
│               └── SKILL.md      # сам скил
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
