# YaMDb
 ![example workflow](https://github.com/niktere12321/yamdb_final/actions/workflows/main.yml/badge.svg)
### Описание
Проект собирает отзывы пользователей на произведения. Каждому произведению могут быть присвоены категория и жанры. Пользователи оставляют к произведениям текстовые отзывы и ставят оценку. Из пользовательских оценок формируется рейтинг. Сами произведения в YaMDb не хранятся.  
Ресурсы API YaMDb:
- **auth**: аутентификация;
- **users**: пользователи;
- **titles**: произведения, к которым пишут отзывы;
- **categories**: категории произведений;
- **genres**: жанры произведений, одно произведение может быть привязано к нескольким жанрам;
- **reviews**: отзывы на произведения;
- **comments**: комментарии к отзывам

### Технологии
- Python 3.8.9
- Django 2.2.16

### Запуск проекта в dev-режиме
- Клонируйте репозиторий и перейдите в папку проекта:
```
git clone https://github.com/niktere12321/infra_sp2.git
```
- Создать и заполнить по образцу .env-файл
```
DB_NAME=<...>
POSTGRES_USER=<...>
POSTGRES_PASSWORD=<...>
DB_HOST=<...>
DB_PORT=<...>
```
```
cd infra_sp2; cd infra
```
- Запустить контейнеры Docker в папке с файлом docker-compose.yaml:
```
docker-compose up -d --build
```
- Выполнить миграции внутри проекта:
```
docker-compose exec web python manage.py migrate
```
- Создать Супер Пользовтеля:
```
docker-compose exec web python manage.py createsuperuser
```
- Подключить статику:
```
docker-compose exec web python manage.py collectstatic --no-input
```

### Примеры запросов

Получение JWT-токена.

```POST /api/v1/auth/token/```

request sample
```
{
    "username": "string",
    "confirmation_code": "string"
}
```

response sample
```
{
    "token": "string"
}
```

Добавление произведения.

```POST /api/v1/titles/```

request sample
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

response sample
```
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

Получение списка всех категорий.

```GET /api/v1/categories/```

response sample
```
[
    {
        "count": 0,
        "next": "string",
        "previous": "string",
        "results": [
            {
                "name": "string",
                "slug": "string"
            }
        ]
    }
]
```

Частичное обновление комментария к отзыву.

```PATCH /api/v1/titles/{title_id}/reviews/{review_id}/comments/{comment_id}/```

request sample
```
{
    "text": "string"
}
```

response sample
```
{
    "id": 0,
    "text": "string",
    "author": "string",
    "pub_date": "2022-02-05T18:15:22Z"
}
```

### Автор
Nikita Terekhov
