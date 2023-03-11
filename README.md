![example workflow](https://github.com/IlDezmond/yamdb_final/actions/workflows/yamdb_workflow.yml/badge.svg)
# yamdb-final
[comment]: <> (Документация работает. Работала она у меня и в прошлый раз.)
## Описание
Проект YaMDb собирает отзывы пользователей на различные произведения.

## Как запустить проект

>*Клонировать репозиторий и перейти в него в командной строке:*


* ```bash
  git clone git@github.com:IlDezmond/infra_sp2.git
  ```

* ```bash
  cd api_yamdb/infra
  ```
  
>*Настроить переменные окружения в файле `.env` по пути `api_yamdb/infra`* <br>
>*Пример файла `example.env` находится там же`*

>*Собрать и запустить докер-контейнеры:*

* ```bash
  docker-compose up -d
  ```

>*Выполнить миграции, собрать статику, создать суперпользователя:*

* ```bash
  docker-compose exec web python manage.py migrate
  docker-compose exec web python manage.py collectstatic --no-input
  docker-compose exec web python manage.py createsuperuser
  ```

>*Открыть проект в браузере:*

* ```bash
  http://localhost
  ```

>*Для загрузки тестовых данных в БД, выполните команду в контейнере web:*

* ```bash
    python manage.py load_csv
  ```

## Примеры работы с API

### GET запрос. Получение списка произведений

```URL
http://localhost/api/v1/titles/
```

```JSON
    {
        "count": 0,
        "next": "string",
        "previous": "string",
        "results": [
            {
                "id": 0,
                "name": "string",
                "year": 0,
                "rating": 0,
                "description": "string",
                "genre": [
                    {
                        "name": "string",
                        "slug": "string"
                    }
                ],
                "category": {
                    "name": "string",
                    "slug": "string"
                }
            }
        ]
    }
```

### POST запрос. Добавление произведения. Права доступа: Администратор

```URL
http://localhost/api/v1/titles/
```

>*request:*

```JSON
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

>*response:*

```JSON
    {
        "id": 0,
        "name": "string",
        "year": 0,
        "rating": 0,
        "description": "string",
        "genre": [
            {
                "name": "string",
                "slug": "string"
            }
        ],
        "category": {
            "name": "string",
            "slug": "string"
        }
    }
```

### POST запрос. Регистрация нового пользователя

```URL
http://localhost/api/v1/auth/signup/
```

>*request:*

```JSON
    {
        "email": "user@example.com",
        "username": "string"
    }
```

>*response:*

```JSON
    {
        "email": "string",
        "username": "string"
    }
```

### POST запрос. Получение JWT-токена пользователем для доступа к API

```URL
http://localhost/api/v1/auth/token/
```

>*request:*

```JSON
    {
        "username": "string",
        "confirmation_code": "string"
    }
```

>*response:*

```JSON
    {
        "token": "string"
    }
```

### Полная документация находится по адресу

```URL
http://localhost/redoc/
```
