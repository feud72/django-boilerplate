## Installation

### pipenv

```bash
pipenv install --python $(which python3) 
```

If error occur in install "black", put below to your Pipfile.

```
[pipenv]
allow_prereleases = true
```

```bash
pipenv install --dev
```

### .env

```bash
touch .env
```

```
DJANGO_SECRET_KEY="{{ YOUR_DJANGO_SECRET_KEY }}"
DJANGO_DB_ENGINE="{{ YOUR_DJANGO_DB_ENGINE }}"
DJANGO_DB_NAME="{{ YOUR_DJANGO_DB_NAME }}"
DJANGO_DB_USER="{{ YOUR_DJANGO_DB_USER }}"
DJANGO_DB_PASSWORD="{{ YOUR_DJANGO_DB_PASSWORD }}"
DJANGO_DB_HOST="{{ YOUR_DJANGO_DB_HOST }}"
DJANGO_DB_PORT="{{ YOUR DJANGO_DB_PORT }}"

AWS_REGION="ap-northeast-2"
AWS_STORAGE_BUCKET_NAME="{{ YOUR_AWS_S3_BUCKET_NAME }}"
AWS_ACCESS_KEY_ID="{{ YOUR_AWS_ACCESS_KEY_ID }}"
AWS_SECRET_ACCESS_KEY="{{ YOUR_AWS_SECRET_ACCESS_KEY }}"
```

### database settings (postgresql)

Caution : "dbname" and "user" may be different with YOUR_DJANGO_DB_NAME and YOUR_DJANGO_DB_USER.

```
psql "host={{ YOUR_DJANGO_DB_HOST }}  port= {{ YOUR_DJANGO_DB_PORT }} dbname={{ DB_NAME }} user={{ DB_USER }}"
```

```
create database {{ YOUR_DJANGO_DB_NAME }};

CREATE DATABASE

create user {{ YOUR_DJANGO_DB_USER }} with password '{{ YOUR_DJANGO_DB_PASSWORD }}';

CREATE ROLE

alter role {{ YOUR_DJANGO_DB_USER }} set client_encoding to 'utf-8';

ALTER ROLE

alter role {{ YOUR_DJANGO_DB_USER }} set timezone to 'Asia/Seoul';

ALTER ROLE

grant all privileges on database {{ YOUR_DJANGO_DB_NAME }} to {{ YOUR_DJANGO_DB_USER }};

GRANT

\q
```

### migrate

```bash
(pipenv shell) python manage.py migrate
```


## Deploy

### zappa init

```bash
zappa init
```

If your stage is "dev", you should input django settings to "config.dev".

If your stage is "production", you should input django settings to "config.production".

```bash
zappa deploy dev
```

### AWS Lambda environment setting

Enter your AWS Lambda console, and put your django environment.

### zappa update

```bash
zappa update dev
```

If your stage is "production", you could run it with command "zappa update production".

If deploy succeeded, you can get the URL. You could put it at "ALLOWED_HOSTS" in your config/dev.py or production.py file.
