# Project 
## Структура проекта
```bash
project/
|---docs/ # документация
|	|---design/ # интерфейс (исходный файл + экспорт png)
|	|---dia_src/ # исходные файлы для диаграмм
|	|---dia_dist/ # файлы диаграмм (svg, png), создаются автоматически
|	|---tech_req.md # ТЗ
|   |--- ... # много разных файлов, в голове держать ничего не нужно
|---src/ # папка с исходными кодами подпроектов
|   |---server/ # backend python
|   |   |---.venv/ # виртуальное окружение
|   |   |---src/ # исходные файлы серверного приложения
|   |   |---.env # переменные окружения
|   |   |---pyproject.toml # конфигурация проекта
|   |---client/ # frontend angular
|   |   |---dist/ # zip-архив скомпилированного приложения
|   |   |---node_modules/ # виртуальное окружение
|   |   |---src/ # исходные файлы клиентского приложения
|   |   |---src-tauri/
|   |   |---angular.json # конфигурация проекта
|   |   |---package.json # зависимости
|   |---setup/ # скрипты установки
|   |   |---main.py # начальный скрипт для выбора задачи
|   |--- ...
|---README.md
```

## Документация

Текстовые файлы в формате markdown. Редактировать можно в простом блокноте, есть спец. редакторы:
- [Obsidian.md](https://obsidian.md/)
- [Typora](https://typora.io/)
- ...

Дизайн - [lunacy](https://icons8.ru/lunacy) Без фанатизма, главное отобразить логику работы пользователя с системой.

Наилучший формат для диаграмм - svg (открытый, поддерживается вебом). Можно редактировать, например, в [Inkscape](https://inkscape.org/ru/).

Диаграммы проще создавать в тексте, и автоматически генерировать изображения.

Полезные диаграммы:
- [C4](https://c4model.com/) - архитектура проекта
- [mermaid erDiagram](https://mermaid-js.github.io/mermaid/#/entityRelationshipDiagram) - схема БД
- [mermaid stateDiagram](stateDiagram) - диаграмма состояний

Преобразовать в изображения можно с помощью [kroki](https://kroki.io/). Пакет для питона, который делает [автоматически](https://github.com/Konstantin-Dudersky/konstantin_docs).

## Исходный код
Jetbrains хорош, но в виду неопределенности разработка кода в открытом и бесплатном редакторе [Visual Studio Code](https://code.visualstudio.com/).

Операционная система - Linux или MacOS, Windows не лучший выбор.

### Server
Основной язык - python актуальной версии (сейчас 3.10).

Управление зависимостями проекта - [poetry](https://python-poetry.org/) Настройки проекта по-максимуму в pyproject.toml.

Линтеры:
- pylance (type checking в режиме strict). mypy не нужен - pylance работает быстрее и лучше.
- pylint
- flake8 с набором плагинов (см pyproject.toml)

Форматирование кода с помощью black. Макс. число символов в строке - 80.

Компоненты:
- [sqlalchemy](https://www.sqlalchemy.org/) - ORM для работы с БД. + драйвера для подключения к БД ([psycopg2](https://pypi.org/project/psycopg2/), ...). 
- [alembic](https://alembic.sqlalchemy.org/en/latest/) - для миграций БД
- [fastapi](https://fastapi.tiangolo.com/) - создания REST-сервиса для обмена со сторонними системами (1С, веб-интерфейс, ...). Работает через веб-сервер [uvicorn](https://www.uvicorn.org/).
- [pydantic](https://pydantic-docs.helpmanual.io/) - валидация данных. Также управление переменными окружения (хранятся в файле .env).
- [asyncua](https://github.com/FreeOpcUa/opcua-asyncio) - если требуется подключение через OPC UA.

Базы данных:
- [SQLite](https://www.sqlite.org/index.html) - для небольших объемов
- [PostgreSQL](https://www.postgresql.org/) - для любых объемов
- [TimescaleDB](https://www.timescale.com/) - для временных данных, расширение к PostgreSQL

### Client
Наболее универсальное решение на сегодняшний день - веб.

Фреймворк - [Angular](https://angular.io/). Язык Typescript.

Пакеты:
- [primeng](https://www.primefaces.org/primeng/) - библиотека компонентов
- [primeflex](https://www.primefaces.org/primeflex/) - CSS верстка
- [rxjs](https://rxjs.dev/) - библиотека для реактивности
- [plotly](https://plotly.com/javascript/) - графики
- [fontawesome](https://fontawesome.com/icons) - шрифт иконок, есть бесплатная версия

Можно упаковывать как приложение для рабочего стола с помощью [tauri](https://tauri.app/).

Форматирование кода с помощью Prettier. Табуляция 4 пробела.