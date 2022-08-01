
![Yamdb Workflow Status](https://github.com/lapanthera161/yamdb_final/actions/workflows/yamdb_workflow.yaml/badge.svg?branch=master&event=push)
# API_YAMDB 
REST API проект для сервиса YaMDb — сбор отзывов о фильмах, книгах или музыке. 

Проект развернут по адресу: http://51.250.19.59/admin
## Описание 
 
Проект YaMDb собирает отзывы пользователей на произведения. 
Произведения делятся на категории: «Книги», «Фильмы», «Музыка». 
Список категорий  может быть расширен. 
## Как запустить проект: 
- Все описанное ниже относится к ОС Linux. 
- Клонируем репозиторий и и переходим в него: 
```bash 
git clone git@github.com:lapanthera161/yamdb_final.git
cd yamdb_final 
cd api_yamdb 
``` 
 
Создаем и активируем виртуальное окружение: 
```bash 
python3 -m venv venv
source /venv/bin/activate (source /venv/Scripts/activate - для Windows) 
python -m pip install --upgrade pip 
``` 
 
Ставим зависимости из requirements.txt: 
```bash 
pip install -r requirements.txt 
``` 

Переходим в папку с файлом docker-compose.yaml: 
```bash 
cd infra 
``` 
 
Поднимаем контейнеры (infra_db_1, infra_web_1, infra_nginx_1): 
```bash 
docker-compose up -d --build 
``` 

Выполняем миграции: 
```bash 
docker-compose exec web python manage.py makemigrations reviews 
``` 
```bash 
docker-compose exec web python manage.py migrate --run-syncdb
``` 

Создаем суперпользователя: 
```bash 
docker-compose exec web python manage.py createsuperuser 
``` 

Србираем статику: 
```bash 
docker-compose exec web python manage.py collectstatic --no-input 
``` 

Создаем дамп базы данных (нет в текущем репозитории): 
```bash 
docker-compose exec web python manage.py dumpdata > fixtures.json 
``` 

Останавливаем контейнеры: 
```bash 
docker-compose down -v 
``` 

### Шаблон наполнения .env (не включен в текущий репозиторий) расположенный по пути infra/.env 
``` 
DB_ENGINE=django.db.backends.postgresql 
DB_NAME=postgres 
POSTGRES_USER=postgres 
POSTGRES_PASSWORD=postgres 
DB_HOST=db 
DB_PORT=5432 
``` 
## Разработчики:


```
https://github.com/Lapanthera161
Произведения и категории
```

```
https://github.com/vladkataev
Отзывы и комментарии
```
