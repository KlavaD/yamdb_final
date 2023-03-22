![test](https://github.com/KlavaD/yamdb_final/actions/workflows/yamdb_workflow.yml/badge.svg)
# Проект API_YAMDB собирает отзывы пользователей на различные произведения. Docker-контейнер. CI и CD проекта api_yamdb
Проект создавали:
* ### Клавдия Дунаева
  модели, view и эндпойнты для
  * произведений,
  * категорий,
  * жанров;
  
  упаковка в контейнер

* ### Андрей Мельников
  * система регистрации и аутентификации,
  * права доступа,
  * работа с токеном,
  * система подтверждения через e-mail.

* ### Николай Артемьев
  модели, view и эндпойнты для
  * отзывов,
  * комментариев,
  * рейтинг произведений.
### Как запустить проект:

В данном проекте использованы технологии:
Python, Django, DRF, Api, Postman

**Как запустить проект:**

Клонировать репозиторий и перейти в него в командной строке:

```
git clone https://github.com/KlavaD/infra_sp2
```

**Описание команд для запуска приложения в контейнерах**

Создайте файл .env с переменными окружения для работы с базой данных:
```
DB_ENGINE=django.db.backends.postgresql
DB_NAME=< имя базы данных>
POSTGRES_USER=<логин для подключения к базе данных>
POSTGRES_PASSWORD=<пароль для подключения к БД (установите свой)>
DB_HOST=< название сервиса (контейнера)>
DB_PORT=5432 # порт для подключения к БД 
```
Запустите контейнер из папки infra/
```
docker-compose up -d --build
```

Выполните следующие команды:
```
docker-compose exec web python manage.py migrate
docker-compose exec web python manage.py createsuperuser
docker-compose exec web python manage.py collectstatic --no-input
```
Сделать импорт из csv файлов:

```
docker-compose exec web python manage.py addcsv
```


## Примеры запросов: ##
Регистрация нового пользователя:
>**POST** http://127.0.0.1/api/v1/signup/

Для получения токена отправьте логин и код, который пришел вам на электронную почту:
>**POST** http://127.0.0.1/api/v1/auth/token/

Получение списка произведений:
>**GET** http://127.0.0.1/api/v1/titles/

Создание публикации (только администратор):
>**POST** http://127.0.0.1/api/v1/titles/
> 
```
{
"name": "string",
"year": 0,
"description": "string",
"genre": [
"string"
],
"category": "string"
}
```

Получение списка категорий:
>**GET** http://127.0.0.1/api/v1/categories/

Получение списка жанров:
>**GET** http://127.0.0.1/api/v1/genre/

Просмотр отзывов на произведение:
>**GET** http://127.0.0.1/api/v1/titles/{title_id}/reviews/

Создание отзывов на произведение:
>**POST** http://127.0.0.1/api/v1/titles/{title_id}/reviews/
```
{
"text": "string",
"score": 1
}
```

Просмотр комментариев к отзыву:
>**GET** http://127.0.0.1/api/v1/titles/{title_id}/reviews/{review_id}/commenta/

Создание комментария к отзыву:
>**Post** http://127.0.0.1/api/v1/titles/{title_id}/reviews/{review_id}/commenta/
```
{
"text": "string"
}
```
Остальные запросы можно посмотреть в документации для API Yamdb:
> http://127.0.0.1/redoc/
