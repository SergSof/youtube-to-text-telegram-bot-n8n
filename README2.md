# YouTube to Text Telegram Bot (n8n)

n8n workflow for a Telegram bot that processes YouTube links and returns:

- short summary
- structured summary
- full transcript as a `.txt` file

The workflow first tries to use YouTube subtitles. If subtitles are unavailable, it downloads the video audio, transcribes it, and then generates summaries.

## Features

- Accepts YouTube links from Telegram
- Validates URLs
- Detects live streams and rejects them
- Extracts subtitles when available
- Falls back to audio transcription when subtitles are missing
- Generates:
  - short summary
  - structured summary
  - full transcript
- Sends transcript back as a TXT document
- Uses configurable working directory via environment variable

## Workflow overview

1. Telegram bot receives a YouTube link
2. Workflow validates the URL
3. Checks whether the link is a live stream
4. Tries to fetch subtitles
5. If subtitles exist:
   - reads subtitle file
   - cleans and merges subtitle text
6. If subtitles do not exist:
   - downloads video
   - extracts audio
   - transcribes audio
7. Builds:
   - short summary
   - structured summary
   - transcript TXT
8. Sends results back to Telegram

## Environment

The workflow uses a working directory variable:

```bash
YOUTUBE_WORKDIR=/data/youtube_video
```

======================================================
# YouTube to Text Telegram Bot (n8n)

n8n workflow для Telegram-бота, который обрабатывает YouTube-ссылки и возвращает:

- краткое саммари
- структурированное саммари
- полный текст в виде `.txt` файла

Сначала workflow пытается использовать субтитры YouTube. Если субтитров нет, он скачивает аудио из видео, делает транскрипцию и затем строит саммари.

## Возможности

- Принимает YouTube-ссылки из Telegram
- Валидирует URL
- Определяет прямые эфиры и отклоняет их
- Извлекает субтитры, если они доступны
- Если субтитров нет — переходит к транскрипции аудио
- Формирует:
  - краткое саммари
  - структурированное саммари
  - полный текст
- Отправляет полный текст обратно в Telegram в виде TXT-файла
- Использует настраиваемую рабочую директорию через переменную окружения

## Как работает workflow

1. Telegram-бот получает ссылку на YouTube
2. Workflow валидирует URL
3. Проверяет, не является ли ссылка прямым эфиром
4. Пытается получить субтитры
5. Если субтитры есть:
   - читает файл субтитров
   - очищает и объединяет текст
6. Если субтитров нет:
   - скачивает видео
   - извлекает аудио
   - делает транскрипцию
7. Формирует:
   - краткое саммари
   - структурированное саммари
   - TXT-файл с полным текстом
8. Отправляет результат обратно в Telegram

## Переменные окружения

Workflow использует переменную рабочей директории:

```bash
YOUTUBE_WORKDIR=/data/youtube_video
```
