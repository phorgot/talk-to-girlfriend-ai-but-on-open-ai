# Telegram AI Dating Agent

An AI-powered Telegram agent that helps you craft witty, engaging messages for your conversations. Built with Claude Sonnet, [Nia](https://trynia.ai) semantic search, and a full-featured Telegram MCP integration.

## What It Does

- **Smart Reply Suggestions**: Get AI-powered response suggestions based on conversation context
- **500+ Pickup Lines**: Semantic search through a curated collection of pickup lines indexed with Nia
- **Dating Guides**: Search through guides on how to talk to women, conversation starters, and flirting tips
- **Message Enhancement**: Transform boring messages into witty, engaging ones
- **Full Telegram Access**: Read messages, send replies, manage chats - all through natural language

## Powered by Nia

This agent uses [Nia](https://trynia.ai) as its knowledge retrieval engine. Nia indexes and searches through:
- 500+ curated pickup lines (funny, cheesy, clever, romantic)
- Guides on conversation techniques
- Tips for keeping conversations engaging

You can index your own content by creating a source at [trynia.ai](https://trynia.ai).

## Architecture

```
┌──────────────────┐     ┌──────────────────┐     ┌──────────────────┐
│   CLI Agent      │────▶│  Telegram API    │────▶│    Telegram      │
│  (TypeScript)    │     │   Bridge (Py)    │     │    Servers       │
└──────────────────┘     └──────────────────┘     └──────────────────┘
         │
         ▼
┌──────────────────┐     ┌──────────────────┐
│  Claude Sonnet   │     │    Nia API       │
│   (AI Gateway)   │     │ (trynia.ai)      │
└──────────────────┘     └──────────────────┘
                         - 500+ pickup lines
                         - Dating guides
                         - Conversation tips
```

## Quick Start

### 1. Get Telegram API Credentials

Get your API credentials at [my.telegram.org/apps](https://my.telegram.org/apps).

### 2. Install & Configure

```bash
# Clone the repo
git clone https://github.com/phorgot/talk-to-girlfriend-ai-but-on-open-ai.git
cd talk-to-girlfriend-ai

# Install Python dependencies
uv sync

# Generate Telegram session string
uv run session_string_generator.py

# Configure environment
cp .env.example .env
# Edit .env with your credentials
```

### 3. Start the Telegram API Bridge

```bash
python telegram_api.py
```

This runs a FastAPI server on port 8765 that bridges the TypeScript agent to Telegram.

### 4. Run the AI Agent

```bash
cd agent
bun install
bun run dev
```

## Usage Examples

Once running, interact with natural language:

```
# Reading & Sending
> Show me messages from @her_username
> Send "Hey, I was just thinking about you" to @her_username
> Reply to her last message with something witty

# Reactions
> React to her last message with ❤️
> Send a 🔥 reaction to message 123

# Search & History
> Search our chat for "dinner plans"
> Show me the last 50 messages with her
> Find me a funny pickup line about pizza

# AI Assistance
> What should I reply to her message about coffee?
> Make this message more flirty: "want to hang out tomorrow?"
> Search for tips on how to keep a conversation going

# User Info
> Is she online right now?
> Check her status

# Message Management
> Edit my last message to fix the typo
> Delete message 456
> Forward that meme to @friend
```

### Agent Commands

- `/help` - Show help
- `/clear` - Clear conversation history
- `/status` - Check connection status
- `/quit` - Exit

## Environment Variables

Create a `.env` file in the project root:

```env

TELEGRAM_API_ID=
TELEGRAM_API_HASH=
TELEGRAM_SESSION_STRING=

OPENAI_API_KEY=

NIA_API_KEY=
NIA_CODEBASE_SOURCE=

```

## Alternative: Use as MCP Server

You can also use this as a standalone MCP server with Claude Desktop or Cursor, without the AI agent.

Add to your MCP config (`~/Library/Application Support/Claude/claude_desktop_config.json`):

```json
{
  "mcpServers": {
    "telegram": {
      "command": "uv",
      "args": ["--directory", "/path/to/telegram-mcp", "run", "main.py"]
    }
  }
}
```

This exposes 60+ Telegram tools including messaging, contacts, groups, channels, reactions, and more.

## Available Tools

### Agent Tools (20+)

**Core Messaging**
| Tool | Description |
|------|-------------|
| `getChats` | List all conversations |
| `getMessages` | Read messages from a chat |
| `sendMessage` | Send a message |
| `getChat` | Get chat details |
| `searchContacts` | Search contacts |

**Reactions & Replies**
| Tool | Description |
|------|-------------|
| `sendReaction` | React with ❤️ 🔥 😂 etc |
| `replyToMessage` | Reply to specific messages |

**Edit & Delete**
| Tool | Description |
|------|-------------|
| `editMessage` | Fix typos after sending |
| `deleteMessage` | Remove messages |

**History & Search**
| Tool | Description |
|------|-------------|
| `getHistory` | Get up to 500 messages |
| `searchMessages` | Search chat by text |

**Forward & Pin**
| Tool | Description |
|------|-------------|
| `forwardMessage` | Forward to another chat |
| `pinMessage` | Pin important messages |
| `markAsRead` | Mark messages as read |

**User Info**
| Tool | Description |
|------|-------------|
| `getUserStatus` | Check if user is online |
| `getUserPhotos` | Get profile photos |

**Media**
| Tool | Description |
|------|-------------|
| `searchGifs` | Search for GIFs |

**Nia Search**
| Tool | Description |
|------|-------------|
| `searchPickupLines` | Search indexed pickup lines & dating advice |
| `niaSearch` | General semantic search |
| `webSearch` | Real-time web search |

**AI Tools**
| Tool | Description |
|------|-------------|
| `aiifyMessage` | Transform messages into witty responses |

### MCP Server Tools (60+)
Full Telegram API access including:
- Chat & Group Management (create, invite, admin, ban)
- Messaging (send, reply, edit, delete, forward, pin, reactions)
- Contact Management (add, search, block, import/export)
- Media & Stickers
- Privacy Settings
- And much more...

## Docker

```bash
docker build -t telegram-mcp:latest .
docker compose up --build
```

## Troubleshooting

- **Database lock errors**: Use session string auth instead of file-based
- **Auth errors**: Regenerate session string with `uv run session_string_generator.py`
- **Connection issues**: Check that `telegram_api.py` is running on port 8765
- **Error logs**: Check `mcp_errors.log` for detailed errors

## Security

- Never commit your `.env` or session string
- Session string = full Telegram account access
- All processing is local, data only goes to Telegram API

## Credits

- Built on [telegram-mcp](https://github.com/chigwell/telegram-mcp) by [@chigwell](https://github.com/chigwell)
- Knowledge retrieval powered by [Nia](https://trynia.ai)
- Uses [Telethon](https://github.com/LonamiWebs/Telethon), [MCP](https://modelcontextprotocol.io/), and [Vercel AI SDK](https://sdk.vercel.ai/)
RU
Вот полный перевод и разбор на понятный язык:

---

# Telegram AI Dating Agent

Телеграм-бот с искусственным интеллектом, который помогает писать остроумные и интересные сообщения для переписки. Использует Claude Sonnet, [Nia](https://trynia.ai) для семантического поиска и полноценную интеграцию с Telegram MCP.

---

## Что умеет

* **Умные подсказки ответов**: ИИ предлагает, как ответить, исходя из контекста переписки
* **500+ фраз для знакомств**: Быстрый поиск по готовым фразам и шуткам через Nia
* **Гайды по свиданиям**: Советы по общению, стартеры разговоров, флирт
* **Улучшение сообщений**: Превращает обычные сообщения в интересные и остроумные
* **Полный доступ к Telegram**: Читать, отправлять сообщения, управлять чатами через естественный язык

---

## Nia (поиск знаний)

Используется как движок для поиска:

* 500+ готовых фраз для знакомств (шутки, романтика, умные фразы)
* Гайды по технике общения
* Советы, как поддерживать интересные диалоги

Можно добавить свои материалы, создав источник на [trynia.ai](https://trynia.ai).

---

## Архитектура

```
CLI Agent (TypeScript)
       │
       ▼
Telegram API Bridge (Python) ──▶ Telegram серверы
       │
       ▼
Claude Sonnet (AI Gateway)    Nia API (trynia.ai)
                              - 500+ фраз для знакомств
                              - Гайды по общению
                              - Советы по переписке
```

---

## Быстрый старт

### 1. Получить данные для Telegram API

На [my.telegram.org/apps](https://my.telegram.org/apps) создаёте приложение и берёте:

* API ID
* API Hash

---

### 2. Установить и настроить

```bash
git clone https://github.com/phorgot/talk-to-girlfriend-ai-but-on-open-ai.git
cd talk-to-girlfriend-ai

# Установить зависимости Python
python -m pip install --upgrade pip
python -m pip install fastapi uvicorn telethon python-dotenv

# Сгенерировать строку сессии Telegram
python session_string_generator.py

# Настроить .env файл
copy .env.example .env
# Заполнить .env вашими данными
```

---

### 3. Запустить Telegram API мост (сервер)

```bash
python telegram_api.py
```

* Сервер запустится на порту 8765
* Он позволяет TypeScript-агенту общаться с Telegram

---

### 4. Запустить AI-агента (бот)

```bash
cd agent
bun install
bun run dev
```

* Бот подключается к локальному серверу и Nia/OpenAI

---

## Примеры использования

* **Чтение и отправка сообщений**:

  > Показать мои сообщения от @her_username
  > Отправить "Привет, думал о тебе" @her_username
  > Ответить на последнее сообщение остроумно

* **Реакции**:

  > Поставить ❤️ на последнее сообщение
  > Отправить 🔥 на сообщение 123

* **Поиск и история**:

  > Найти "ужин" в переписке
  > Показать последние 50 сообщений с ней
  > Найти шутливую фразу про пиццу

* **AI-помощь**:

  > Как ответить на сообщение о кофе?
  > Сделать сообщение более флиртующим: "хочешь встретиться завтра?"
  > Найти советы, как поддерживать диалог

* **Информация о пользователе**:

  > Она онлайн сейчас?
  > Проверить статус

* **Управление сообщениями**:

  > Исправить опечатку в последнем сообщении
  > Удалить сообщение 456
  > Переслать мем другу

---

### Команды агента

* `/help` — помощь
* `/clear` — очистить историю
* `/status` — проверить соединение
* `/quit` — выйти

---

## Переменные окружения (.env)

```env
TELEGRAM_API_ID=
TELEGRAM_API_HASH=
TELEGRAM_SESSION_STRING=

OPENAI_API_KEY=

NIA_API_KEY=
NIA_CODEBASE_SOURCE=
```

* В `.env` прописываются все ключи и токены

---

## Альтернатива: использовать как MCP-сервер

Можно подключить к Claude Desktop или Cursor без AI-агента.

Пример конфигурации MCP:

```json
{
  "mcpServers": {
    "telegram": {
      "command": "uv",
      "args": ["--directory", "/path/to/telegram-mcp", "run", "main.py"]
    }
  }
}
```

* Открывает 60+ инструментов Telegram: чаты, группы, сообщения, реакции и т.д.

---

## Инструменты агента

**Сообщения**

* `getChats` — список чатов
* `getMessages` — читать сообщения
* `sendMessage` — отправить сообщение
* `getChat` — информация о чате
* `searchContacts` — поиск контактов

**Реакции и ответы**

* `sendReaction` — реакция (❤️🔥😂)
* `replyToMessage` — ответ на конкретное сообщение

**Редактирование и удаление**

* `editMessage` — исправить опечатку
* `deleteMessage` — удалить

**История и поиск**

* `getHistory` — последние 500 сообщений
* `searchMessages` — поиск по тексту

**Пересылка и закрепление**

* `forwardMessage` — переслать сообщение
* `pinMessage` — закрепить
* `markAsRead` — отметить прочитанным

**Информация о пользователях**

* `getUserStatus` — онлайн/офлайн
* `getUserPhotos` — фото профиля

**Медиа**

* `searchGifs` — поиск GIF

**Поиск через Nia**

* `searchPickupLines` — фразы и советы для свиданий
* `niaSearch` — общий семантический поиск
* `webSearch` — поиск в интернете

**AI-инструменты**

* `aiifyMessage` — превращает сообщение в остроумное

---

## MCP Tools (60+)

Полный доступ к Telegram API: управление чатами, группами, сообщениями, контактами, медиа, приватностью и т.д.

---

## Docker

```bash
docker build -t telegram-mcp:latest .
docker compose up --build
```

---

## Устранение проблем

* **Блокировка базы**: используйте строку сессии, а не файл
* **Ошибки авторизации**: пересоздайте строку сессии `session_string_generator.py`
* **Проблемы соединения**: проверьте, что `telegram_api.py` запущен на порту 8765
* **Логи ошибок**: `mcp_errors.log`

---

## Безопасность

* Не коммитьте `.env` или строку сессии
* Строка сессии = полный доступ к аккаунту Telegram
* Все данные обрабатываются локально, отправляется только в Telegram API

---

## Авторы и технологии

* Построено на [telegram-mcp](https://github.com/chigwell/telegram-mcp)
* Поиск знаний через [Nia](https://trynia.ai)
* Используются Telethon, MCP, Vercel AI SDK

в переводе есть ошибки, смотреть оригинал если что то не понятно,
