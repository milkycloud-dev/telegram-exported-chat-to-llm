# Chat Export to LLM

Конвертер экспортов чатов из **Telegram** и **Discord** в `.docx` для загрузки в [NotebookLM](https://notebooklm.google.com/) и другие LLM-инструменты.

## Возможности

- **Telegram** — парсинг JSON-экспорта (`result.json` из «Export chat history»)
- **Discord** — парсинг HTML-экспорта (`discord-chat.html` из DiscordChatExporter и аналогов)
- Сохранение даты, автора и текста каждого сообщения
- Маркеры вложений: фото, стикеры, голосовые, видео, файлы
- Эмодзи Discord подставляются как текст (`alt` у `<img>`)

## Требования

- Python 3.8+

## Установка

```bash
git clone <url-репозитория>
cd <имя-репозитория>
pip install -r requirements.txt
```

## Использование

Укажите каталог с экспортом чата. Скрипт ищет в нём `result.json` (Telegram) и/или `discord-chat.html` (Discord) и создаёт `.docx` рядом с исходниками.

```bash
python convert_to_llm.py /path/to/chat/export
```

Пример:

```bash
python convert_to_llm.py ~/Downloads/ChatExport_2026-03-28
```

Результат:

| Входной файл | Выходной файл |
|---|---|
| `result.json` | `telegram_chat.docx` |
| `discord-chat.html` | `discord_chat.docx` |

### Отдельные файлы

```bash
# только Telegram
python convert_to_llm.py --telegram /path/to/result.json --telegram-out chat.docx

# только Discord
python convert_to_llm.py --discord /path/to/discord-chat.html --discord-out chat.docx
```

## Как получить экспорт

### Telegram

1. Откройте чат в Telegram Desktop.
2. **⋮ → Export chat history**.
3. Формат: **JSON**, без медиа (достаточно для текста).
4. В каталоге экспорта будет `result.json`.

### Discord

1. Экспортируйте чат через [DiscordChatExporter](https://github.com/Tyrrrz/DiscordChatExporter) или аналог.
2. Формат: **HTML**.
3. Положите `discord-chat.html` в каталог экспорта.

## Формат выходного документа

Каждое сообщение — отдельный абзац:

```
[2026-03-28 14:30:00] Username: текст сообщения [Photo]
```

Дата и имя отправителя выделены **жирным**.

## Структура проекта

```
.
├── convert_to_llm.py   # основной скрипт
├── requirements.txt    # зависимости Python
├── LICENSE             # MIT License
└── README.md
```

## Лицензия

[MIT License](LICENSE) — свободное использование, изменение и распространение с сохранением уведомления об авторских правах.
