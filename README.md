<sub>Заполнениние README.md выполнено с применением разметки [Markdown](https://docs.github.com/ru/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax).</sub>



# Проект YaMDb

__API YaMDb__ представляет собой программный интерфейс социальной сети YamDb, реализованный на архитектуре __REST API__ с применением формата обмена данными __JSON__.

__<details><summary>Технологии</summary>__

- [x] Python
- [x] Django
- [x] Django REST Framework
- [x] JWT
- [x] Nginx
- [x] Gunicorn 
- [x] Docker 

</details>

__<details><summary>Описание</summary>__

Проект YaMDb собирает **отзывы** пользователей на **произведения**. Сами произведения в YaMDb не хранятся, здесь нельзя посмотреть фильм или послушать музыку.

Произведения делятся на **категории**, такие как «Книги», «Фильмы», «Музыка». Например, в категории «Книги» могут быть произведения «Винни-Пух и все-все-все» и «Марсианские хроники», а в категории «Музыка» — песня «Давеча» группы «Жуки» и вторая сюита Баха. Список категорий может быть расширен (например, можно добавить категорию «Изобразительное искусство» или «Ювелирка»).

Произведению может быть присвоен **жанр** из списка предустановленных (например, «Сказка», «Рок» или «Артхаус»).

Добавлять произведения, категории и жанры может только администратор.

Благодарные или возмущённые пользователи оставляют к произведениям текстовые **отзывы** и ставят произведению оценку в диапазоне от одного до десяти (целое число); из пользовательских оценок формируется усреднённая оценка произведения — **рейтинг** (целое число). На одно произведение пользователь может оставить только один отзыв.

Пользователи могут оставлять **комментарии** к отзывам.

Добавлять отзывы, комментарии и ставить оценки могут только аутентифицированные пользователи.

</details>

__<details><summary>Пользовательские роли и права доступа</summary>__
 
-   **Аноним** — может просматривать описания произведений, читать отзывы и комментарии.
-   **Аутентифицированный пользователь (**`user`**)** — может читать всё, как и **Аноним**, может публиковать отзывы и ставить оценки произведениям (фильмам/книгам/песенкам), может комментировать отзывы; может редактировать и удалять свои отзывы и комментарии, редактировать свои оценки произведений. Эта роль присваивается по умолчанию каждому новому пользователю.
-   **Модератор (**`moderator`**)** — те же права, что и у **Аутентифицированного пользователя**, плюс право удалять и редактировать **любые** отзывы и комментарии.
-   **Администратор (**`admin`**)** — полные права на управление всем контентом проекта. Может создавать и удалять произведения, категории и жанры. Может назначать роли пользователям.
-   **Суперюзер Django** должен всегда обладать правами администратора, пользователя с правами `admin`. Даже если изменить пользовательскую роль суперюзера — это не лишит его прав администратора. Суперюзер — всегда администратор, но администратор — не обязательно суперюзер.

</details>

__<details><summary>Документация</summary>__

Документация API доступна по адресу: [http://localhost/redoc/](http://localhost/redoc/).
    
_<details><summary>Примеры запросов</summary>_

 - **Регистрация пользователя в системе:**
POST (c параметрами `username` и `email`)
`/api/v1/auth/signup/`
В ответ сервис **YaMDB** отправляет письмо с кодом подтверждения (`confirmation_code`) на указанный адрес `email`.
- **Получение пользователем токена:**
POST (с параметрами `username` и `confirmation_code`)
 `/api/v1/auth/token/`
```
{
    "username": "testuser1",
    "confirmation_code": "bk3ma8-c56776265de7328a17ef39b9ae5c6ee2"
}
```
В ответе на запрос пользователю приходит `token` (JWT-токен).
```{
    "token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ8.eyJ0b2tlbl90eXBlIjoiYWNjZXNzIiwiZXhwIjoxNjc5Nzc3NjA5LCJqdGkiOiIxYmNlNzVkMDVhOGM0ZjcwODEyMWZkMjU3YjU4OGI2MiIsInVzZXJfaWQiOjJ8.OqelqpS-eLDjBHbKkZshSAQj0SEcOAO-z5oWEh5PGDQ"
}
```
- **Получение списка жанров:**
GET `/api/v1/genres/`
```
{
    "count": 3,
    "next": null,
    "previous": null,
    "results": [
        {
            "name": "Fiction",
            "slug": "fiction"
        },
        {
            "name": "Non-fiction",
            "slug": "non-fiction"
        },
        {
            "name": "Fairytales",
            "slug": "fairytales"
        }
    ]
}
```
- **Получение списка произведений:**
GET `/api/v1/titles/`
- **Получение списка отзывов:**
GET `/api/v1/titles/{title_id}/reviews/`
- **Получение списка комментариев к отзыву:**
GET `/api/v1/ /titles/{title_id}/reviews/{review_id}/comments/`
- **Публикация нового жанра:**
POST `/api/v1/genres/'` - c правами Администратора/Суперпользователя
```
{
    "name": "Fiction",
    "slug": "fiction"
}
```
ответ: 
```
{
    "name": "Fiction",
    "slug": "fiction"
}
```
- **Публикация новой категории:**
POST `/api/v1//categories/'` - c правами Администратора/Суперпользователя
```
{
    "name": "Современная литература",
    "slug": "modern"
}
```
ответ: 
```
{
    "name": "Современная литература",
    "slug": "modern"
}
```
</details>

</details>


__<details><summary>Как развернуть проект (локально)</summary>__

1. Клонировать репозиторий:
    ```
    git clone git@github.com:awesky/infra_sp2.git
    ```
2. Сформировать файл переменных вируального окружения (ENV-файл) и разместить разместить в `/infra/`.
    _<details><summary>Шаблон ENV-файла</summary>_    

        # Django
        SECRET_KEY="<key_value>"
        # Указываем базу данных, с которой будем работать
        DB_ENGINE=django.db.backends.postgresql
        # Задаем имя базы данных
        DB_NAME=postgres
        # Указываем логин для подключения к базе данных
        POSTGRES_USER=postgres
        # Указываем пароль для подключения к БД
        POSTGRES_PASSWORD=passw0rd
        # Указываем название сервиса (контейнера)
        DB_HOST=db
        # Указываем порт для подключения к БД
        DB_PORT=5432

    </details>
    
    
**Дальнейшие шаги выполнять при запущенном Docker.**
    
3. Перейти в каталог, содержащий файл `docker-compose.yaml`, (по-умолчанию: `/infra/`) и выполнить следующую команду:
    
    ```
    docker-compose up -d --build
    ```
    
4. В контейнере `web`:
    
    Выполнить миграции:
    ```
    docker-compose exec web python manage.py makemigrations
    docker-compose exec web python manage.py migrate
    ```
    Создать суперпользователя:
    ```
    docker-compose exec web python manage.py createsuperuser
    ```
    Собрать статику:
    ```
    docker-compose exec web python manage.py collectstatic --no-input
    ```
    
5. Заполнить базу данных:
    
- из существующего дампа (`fixtures.json`):
    
    ```
    docker-compose exec web python manage.py loaddata fixtures.json
    ```
    или
    
- из файла (демонстрационные данные):
    
    ```
    docker-compose exec web python manage.py load_data_from_csv
    ```

</details>

#
Made by:

- [x] [Andrei Bodrov](https://github.com/awesky)
- [x] [Dmitriy Mayorov](https://github.com/dmay92)
- [x] [Valeria Goran](https://github.com/vinni-pushinka)

within [Yandex.Practicum](https://practicum.yandex.ru/) on May 2023
