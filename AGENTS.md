# AGENTS.md — Digitization of Chemical Books Using Machine Vision

Это LaTeX-проект научной статьи. Не код проекта, не монорепа.

## Быстрый старт

```bash
# Включить pre-commit hook (делает PDF + monolith.tex при каждом commit)
git config core.hooksPath .githooks

# Сборка PDF вручную
latexmk -pdf -interaction=nonstopmode -halt-on-error main.tex
```

## Структура

| Путь | Назначение |
|---|---|
| `main.tex` | Точка входа — подключает всё `\input{}`-ами |
| `preamble.tex` / `user_preamble.tex` | Преамбула (пакеты, layout, custom commands) |
| `tit.tex` | Титульная страница (UDC, авторы, affiliation, abstract, keywords) |
| `chapter/` | Файлы-обёртки для разделов (5 шт.), `\input{}`-ят контент из `paragraph/` |
| `paragraph/` | Содержательные параграфы (27 файлов) — здесь пишется текст |
| `thebibliography_ru.tex` / `_en.tex` | Списки литературы (GOST R 7.0.100-2018), **не BibTeX**, ручное `\bibitem{}` |
| `img/` | PNG-изображения (12 шт.) |
| `table/` | Таблицы: `ocr.tex` (точность OCR), `ocsr.tex` (сравнение OCSR-моделей) |

## Pre-commit hook (`.githooks/pre-commit`)

При каждом `git commit`:
1. `latexmk -pdf main.tex` → `main.pdf`
2. `latexpand main.tex` → `monolith.tex` (все `\input{}`-ы инлайн)
3. `git add main.pdf monolith.tex`

Оба артефакта **коммитятся в репозиторий**. Если не нужны, их можно удалить из commit-а вручную.

## Сборка

Только pdflatex (T2A Cyrillic, UTF-8). BibTeX/Biber не используется — библиография вручную через `thebibliography`. Двухколоночная верстка через `multicol`.

## Тесты, линтеры, CI

Отсутствуют. Единственная автоматизация — pre-commit hook выше.

## Стиль и конвенции

- Русскоязычная статья, но раздел References на английском.
- Источники: ГОСТ R 7.0.100-2018, минимум 18 источников.
- Требования журнала: 9–12 стр. A4, Times New Roman 11pt, две колонки.

## Комментарии

Содержимое `main.tex` содержит `\input{}`-ы параграфов, некоторые из них закомментированы — не удалять без необходимости.
