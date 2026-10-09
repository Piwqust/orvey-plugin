# orvey plugin

Картинки и концепты из студии [orvey](https://orvey.angleford.co/connect) прямо в Claude, ChatGPT, Claude Code и Codex.
orvey рисует через ключ вашей студии к моделям (GPT Image 2.5, Nano Banana и другие) и хранит всё, что сделано.

*English below.*

## Что внутри

| Часть | Что делает |
|---|---|
| MCP-сервер `orvey` | `https://mcp.orvey.angleford.co/mcp`: инструменты для модели и виджеты (MCP Apps) — карточки с картинками, выбор концептов, студия на весь экран |
| Навык `orvey-images` | Когда какой инструмент: концепты для открытых задач, черновик → финал, поиск по библиотеке, правила экономии |
| `concepts` | Десять по-настоящему разных концептов на бриф: бесплатная проверка, затем выбор человека |
| `draw` | Одна картинка по описанию: черновик, затем финал |
| `studio` | Открывает студию в чате |

Виджеты рисуются в чате Claude (claude.ai и приложение) и ChatGPT. В терминале (Claude Code, Codex) результат приходит текстом и ссылками.

## Установка

Нужен аккаунт orvey: приглашение даёт администратор студии. При первом подключении откроется вход в orvey — логин,
пароль, «Разрешить». Ключи в конфигах не хранятся.

**Claude Code**

```bash
claude plugin marketplace add Piwqust/orvey-plugin
claude plugin install orvey@orvey
```

Затем `/mcp` → orvey → Authenticate.

**Codex и ChatGPT для компьютера**

```bash
codex plugin marketplace add Piwqust/orvey-plugin
codex plugin add orvey@orvey
codex mcp login orvey
```

**Claude и ChatGPT без плагина** (виджеты в чате): добавьте свой коннектор / приложение с адресом
`https://mcp.orvey.angleford.co/mcp` — пошагово на [orvey.angleford.co/connect](https://orvey.angleford.co/connect).

**Своя студия orvey:** замените адрес в `plugins/orvey/.mcp.json` и `plugins/orvey/mcp.json`.

[Конфиденциальность](https://orvey.angleford.co/privacy) · [Условия](https://orvey.angleford.co/terms)

---

## English

Pictures and concepts from an [orvey](https://orvey.angleford.co/connect?lang=en) studio inside Claude, ChatGPT, Claude Code
and Codex. The plugin connects the orvey MCP server (with MCP Apps widgets: result cards, concept picking, a full-screen
studio) and adds a skill that tells the agent which tool fits which task, plus `concepts`, `draw` and `studio` commands.

You need an orvey account (an invitation from the studio's administrator). The first connection opens an orvey sign-in
page (OAuth); no keys are stored in config files.

```bash
claude plugin marketplace add Piwqust/orvey-plugin
claude plugin install orvey@orvey
```

```bash
codex plugin marketplace add Piwqust/orvey-plugin
codex plugin add orvey@orvey
codex mcp login orvey
```

Widgets show in the Claude and ChatGPT chats; terminals get text and links.
[Privacy](https://orvey.angleford.co/privacy?lang=en) · [Terms](https://orvey.angleford.co/terms?lang=en)
