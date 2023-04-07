![Django-app workflow](https://github.com/TheUncannyMrBean/yamdb_final/actions/workflows/yamdb_workflow.yml/badge.svg)

#Continuous Integration and Continuous Deployment для проекта api_yamdb

Этот проект представляет собой настройку Continuous Integration и Continuous Deployment для приложения api_yamdb, которое было упаковано в контейнеры в предыдущем задании. YaMDb - это онлайн-библиотека отзывов о фильмах, книгах и музыке. Этот проект предоставляет возможность пользователям оставлять отзывы на произведения и оценивать их. Администраторы проекта могут добавлять новые произведения и категории, а также управлять пользователями и модерировать отзывы. Проект был упакован в контейнер.

## Функциональность проекта

- Автоматический запуск тестов при каждом пуше в репозиторий.
- Обновление образов приложения на Docker Hub при успешном прохождении тестов.
- Автоматический деплой приложения на боевой сервер при каждом пуше в главную ветку main.
- Отправка сообщения об успешном деплое в Telegram

## Подготовка для запуска Workflow

Откройте терминал и перейдите в каталог, в который планируете скопировать репозиторий
```
cd 
```
Клонируйте репозиторий:
```
git@github.com:TheUncannyMrBean/yamdb_final.git
```
Перейдите в корневую директорию проекта:
```
cd yamdb_final
```

2. Создайте и активируйте виртуальное окружение и обновите pip.
```
python3 -m venv venv
. venv/bin/activate
python3 -m pip install --upgrade pip
```

3. Отредактируйте файл `nginx/default.conf`, вписав в строке `server_name` IP своего виртуального сервера.  
Скопируйте подготовленные файлы `docker-compose.yaml` и `nginx/default.conf` из вашего проекта на сервер:
```
scp docker-compose.yaml <username>@<host>/home/<username>/docker-compose.yaml
sudo mkdir nginx
scp default.conf <username>@<host>/home/<username>/nginx/default.conf
```

4. В репозитории на GitHub добавьте данные в Settings - Secrets and variables - Actions:

```
DOCKER_USERNAME - имя пользователя в DockerHub
DOCKER_PASSWORD - пароль пользователя в DockerHub
HOST - ip-адрес сервера
USER - пользователь
SSH_KEY - приватный ssh-ключ (публичный должен быть на сервере)
PASSPHRASE - кодовая фраза для ssh-ключа
DB_ENGINE - django.db.backends.postgresql
DB_NAME - postgres (по умолчанию)
POSTGRES_USER - postgres (по умолчанию)
POSTGRES_PASSWORD - postgres (по умолчанию)
DB_HOST - db
DB_PORT - 5432
SECRET_KEY - секретный ключ приложения django (находится в текстовом документе settings.py, без скобок)
TELEGRAM_TO - id своего телеграм-аккаунта (можно узнать у @userinfobot, команда /start)
TELEGRAM_TOKEN - токен бота (получить токен можно у @BotFather, /token, имя бота)
```

5. Запустите Workflow проекта, внеся свои изменения:
```
git add .
git commit -m "..."
git push
```

## Как развернуть проект на виртуальном сервере:
Установите соединение с сервером:
```
ssh username@server_address
```
Проверьте статус nginx:
```
sudo service nginx status
```
Если nginx запущен, остановите его:
```
sudo systemctl stop nginx
```
Установите Docker и Docker-compose:
```
sudo apt install docker.io
sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
```
Проверьте корректность установки Docker-compose:
```
sudo  docker-compose --version
```
Создайте папку `nginx`:
```
mkdir nginx
```

### Проверьте работоспособность адреса развёрнутого проекта:
http://84.201.133.200/admin/

### Контакты
Если у вас есть какие-либо вопросы или предложения по проекту, вы можете связаться со мной по следующим контактным данным:

- Email: diuk2001@yandex.ru
- Telegram: @sashagolikov


