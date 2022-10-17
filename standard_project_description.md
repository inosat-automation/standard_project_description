# Standard project description 

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

В качестве IDE подходит [Visual Studio Code](https://code.visualstudio.com/).

### Back-end

Основной язык - python.

Управление зависимостями проекта - [poetry](https://python-poetry.org/).

Компоненты:
- [sqlalchemy](https://www.sqlalchemy.org/) - ORM для работы с БД. + драйвера для подключения к БД ([psycopg2](https://pypi.org/project/psycopg2/), psycopg3, ...). 
- [alembic](https://alembic.sqlalchemy.org/en/latest/) - для миграций БД
- [fastapi](https://fastapi.tiangolo.com/) - создания REST-сервиса для обмена со сторонними системами (1С, веб-интерфейс, ...). Работает через веб-сервер [uvicorn](https://www.uvicorn.org/).
- [pydantic](https://pydantic-docs.helpmanual.io/) - валидация данных. Также управление переменными окружения (хранятся в файле .env).
- [pandas](https://pandas.pydata.org/) - обработка табличных данных

Отладка с помощью [debugpy](https://github.com/microsoft/debugpy).

Линтеры:
- [pyright](https://github.com/microsoft/pyright) (type checking в режиме strict).
- flake8 с набором плагинов ([wemake-python-styleguide](https://github.com/wemake-services/wemake-python-styleguide))

Форматирование кода с помощью [black](https://black.readthedocs.io/en/stable/). Макс. число символов в строке - 80.

Создание документации по исходному коду - [sphinx](https://www.sphinx-doc.org/en/master/).

### Front-end

Наболее универсальное решение на сегодняшний день - веб.

Фреймворк - [Angular](https://angular.io/). Язык Typescript.

Пакеты:

- [primeng](https://www.primefaces.org/primeng/) - библиотека компонентов
- [primeflex](https://www.primefaces.org/primeflex/) - CSS верстка
- [rxjs](https://rxjs.dev/) - библиотека для реактивности
- [plotly](https://plotly.com/javascript/) - графики
- [fontawesome](https://fontawesome.com/icons) - шрифт иконок, есть бесплатная версия

Можно упаковывать как приложение для рабочего стола с помощью [tauri](https://tauri.app/).

Форматирование кода с помощью Prettier.

Создание документации по исходному коду - [compodoc](https://compodoc.app/).

### Базы данных

#### [SQLite](https://www.sqlite.org/index.html)

Можно использовать для небольших объемов данных на встраиваемых компьютерах.

#### [PostgreSQL](https://www.postgresql.org/)

Полноценная серверная БД.

Есть расширения для специфических задач. Например, временн**ы**е данные удобно обрабатывать с помощью [TimescaleDB](https://www.timescale.com/)

Веб-интерфейс для мониторинга - [pgAdmin](https://www.pgadmin.org/)

Резервное копирование данных:
- периодическое создание резервных копий с помощью pg_dump
- непрерывная репликация на резервный сервер
- создание высокодоступного кластера с помощью сторонних решений - например, [patroni](https://github.com/zalando/patroni)

### Коммуникация с устройствами

- Siemens S7 - [python-snap7](https://github.com/gijzelaerr/python-snap7)
- OPC UA - [asyncua](https://github.com/FreeOpcUa/opcua-asyncio)
- Modbus TCP / RTU - [pymodbus](https://github.com/riptideio/pymodbus)
- SNMP - [pysnmp](https://github.com/pysnmp/pysnmp)
- сторонние HTTP API - [httpx](https://github.com/encode/httpx), [websockets](https://websockets.readthedocs.io/en/stable/)

### Структура проекта
```py
project/
|---docs/ # документация
|   |---design/ # интерфейс (исходный файл + экспорт png)
|   |---dia_src/ # исходные файлы для диаграмм
|   |---dia_dist/ # файлы диаграмм (svg, png), создаются автоматически
|   |---tech_req.md # ТЗ
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

## Установка

### Операционная система

Предпочтительно использовать операционые системы на базе Linux. В качестве аппаратной части можно использовать:

- обычные компьютеры на базе процессоров Intel/AMD
- встраиваемые компьютеры на базе ARM (например, Siemens IOT2050)
- панельные компьютеры

### Виртуализация

Для больших систем удобно использовать виртуализацию. В качестве системы виртуализации можно использовать бесплатный [Proxmox Virtual Environment](https://www.proxmox.com/en/proxmox-ve):

- поддержка гипервизора KVM (Kernel-based Virtual Machine) - гостевые системы Windows / Linux.
- поддержка контейнеров LXC (Linux Containers) - только Linux.
- удобное создание резервных копий с помощью [Proxmox Backup Server](https://www.proxmox.com/en/proxmox-backup-server).
- веб-интерфейс

### Контейнеризация

Отдельные части приложения (сервисы) упаковываются в контейнеры [Docker](https://www.docker.com/).

Сборка образов (в т.ч. мультиплатформенная) с помощью [buildkit](https://github.com/moby/buildkit).

Запуск на целевой системе с помощью [docker compose](https://docs.docker.com/compose/).

Веб-интерфейс для управления - [portainer](https://www.portainer.io/).
