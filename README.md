[![Yamdb workflow](https://github.com/igor-isht/yamdb_final/actions/workflows/yamdb_workflow.yml/badge.svg)](https://github.com/igor-isht/yamdb_final/actions/workflows/yamdb_workflow.yml)



# Проект YaMDb. Приложение reviews и его API
Проект YaMDb собирает отзывы пользователей на различные произведения.

Используемый стек: Django REST Framework, Docker, PostgreSQL, Nginx

## Установка. Как запустить проект 🛫 :

---
- Клонировать репозиторий и перейти в него в командной строке:

```
git clone https://github.com/igor-isht/infra_sp2.git
```

```
cd infra_sp2/infra
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
либо, для завершения и удаления контейнеров (но не образов!):

```
docker-compose down -v 
```

При необходимости, установите собственные настройки для БД, создав .env файл в корне проекта со следующей структурой (при отсутствии файла используются значения по умолчанию):

```
# .env
DB_NAME=NAME
POSTGRES_PASSWORD=PASSWORD
```

---
## Пользовательские роли
- Аноним - может просматривать описания произведений, читать отзывы и комментарии.
- Аутентифицированный пользователь (user) — может читать всё, как и Аноним, может публиковать отзывы и ставить оценки произведениям (фильмам/книгам/песенкам), может комментировать отзывы; может редактировать и удалять свои отзывы и комментарии, редактировать свои оценки произведений. Эта роль присваивается по умолчанию каждому новому пользователю.
- Модератор (moderator) — те же права, что и у Аутентифицированного пользователя, плюс право удалять и редактировать любые отзывы и комментарии.
- Администратор (admin) — полные права на управление всем контентом проекта. Может создавать и удалять произведения, категории и жанры. Может назначать роли пользователям.
- Суперюзер Django должен всегда обладать правами администратора, пользователя с правами admin. Даже если изменить пользовательскую роль суперюзера — это не лишит его прав администратора. Суперюзер — всегда администратор, но администратор — не обязательно суперюзер.

## Самостоятельная регистрация новых пользователей
1. Пользователь отправляет POST-запрос с параметрами email и username на эндпоинт `/api/v1/auth/signup/`
2. Сервис YaMDB отправляет письмо с кодом подтверждения (confirmation_code) на указанный адрес email
3. Пользователь отправляет POST-запрос с параметрами username и confirmation_code на эндпоинт `/api/v1/auth/token/`, в ответе на запрос ему приходит token (JWT-токен)
4. В результате пользователь получает токен и может работать с API проекта, отправляя этот токен с каждым запросом
5. После регистрации и получения токена пользователь может отправить PATCH-запрос на эндпоинт `/api/v1/users/me/` и заполнить поля в своём профайле (описание полей — в документации)

## Создание пользователя администратором
Пользователя может создать администратор — через админ-зону сайта или через POST-запрос на специальный эндпоинт api/v1/users/ (описание полей запроса для этого случая — в документации). В этот момент письмо с кодом подтверждения пользователю отправлять не нужно.
После этого пользователь должен самостоятельно отправить свой email и username на эндпоинт /api/v1/auth/signup/ , в ответ ему должно прийти письмо с кодом подтверждения.
Далее пользователь отправляет POST-запрос с параметрами username и confirmation_code на эндпоинт /api/v1/auth/token/, в ответе на запрос ему приходит token (JWT-токен), как и при самостоятельной регистрации.


