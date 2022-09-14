[![Yamdb workflow](https://github.com/igor-isht/yamdb_final/actions/workflows/yamdb_workflow.yml/badge.svg?branch=master)](https://github.com/igor-isht/yamdb_final/actions/workflows/yamdb_workflow.yml)


# Проект YaMDb. Приложение reviews и его API
Проект YaMDb собирает отзывы пользователей на различные произведения.

Используемый стек: Django REST Framework, Docker, PostgreSQL, Nginx, GitHub Actions

## Установка. Как запустить проект 🛫 :

---
- Клонировать репозиторий и перейти в него в командной строке:

```
git clone https://github.com/igor-isht/yamdb_final.git
```

```
cd yamdb_final/infra
```

Cоздать файл с переменными окружения .env с настройками БД и со следующими ключами
(можно создать пустой файл, будут применены настройки по умолчанию):


```
DB_ENGINE=django.db.backends.postgresql

DB_NAME=your_db_name 

POSTGRES_USER=your_user

POSTGRES_PASSWORD=your_password

DB_HOST=your_host

DB_PORT=5432

SECRET_KEY=Your_secret_key
```

- Запустить docker-compose (необходим Docker Desktop):

```
docker-compose up -d
```

Готово!


Для завершения работы контейнеров введите:

```
docker-compose stop
```
для удаления контейнеров и образов:

```
docker system prune -f 
```




## Документация

После запуска контейнеров документация будет доступна по адресу 127.0.0.1/redoc/

Реализованы JWT-авторизация, пагинация, поиск, разграничение прав доступа


Примеры реализованных эндпойтов:
  
127.0.0.1/api/v1/titles/ (GET/POST) - получение списка произведений/добавление нового произведения

127.0.0.1/api/v1/titles/{title_id}/ (GET/PATCH/DELETE) - получение информации о произведении/рактирование/удаление


127.0.0.1/api/v1/titles/{title_id}/reviews/ (GET/POST) - список отзывов/добавление нового

127.0.0.1/api/v1/titles/{title_id}/reviews/{review_id}/ (GET/PATCH/DELETE) - информация об отзыве/редактирование/удаление


127.0.0.1/api/v1/titles/{title_id}/reviews/{review_id}/comments/ (GET/POST)  - список комментариев/добавление нового

127.0.0.1/api/v1/titles/{title_id}/reviews/{review_id}/comments/{comment_id}/ (GET/PATCH/DELETE)


## Авторы
Над проектом работали:

[@DenielMay](https://github.com/DenielMay) - регистрация и аутентификация пользователей, права доступа, работа с токеном

[@igor-isht](https://github.com/igor-isht) - настройка эндпойнтов для жанров, произведений и категорий

[@blackworse8](https://github.com/blackworse8) - настройка эндпойнтов для отзывов и комментариев

[@yandex-praktikum](https://github.com/yandex-praktikum) - юнит-тесты
