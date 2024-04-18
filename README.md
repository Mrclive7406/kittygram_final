# Kittygram final

##Установка
1. Клонируйте репозиторий на свой компьютер:
```bash
 git clone https://github.com/devlili/kittygram_final.git
```
```bash
cd kittygram
```
##Запуск
1. Подготовим виртуальное окружение в директории проекта создадим файл .env:
```bash
nano .env
```
2. Добавляем следующие переменные:
```nano
POSTGRES_DB=kittygram
POSTGRES_USER=kittygram_user
POSTGRES_PASSWORD=kittygram_password
DB_HOST=db
DB_PORT=5432
SECRET_KEY=...
DEBUG=... # True/False
ALLOWED_HOSTS=127.0.0.1,localhost
```
3. Устанавливаем к Docker утилиту Docker Compose:
```bash
sudo apt update
sudo apt-get install docker-compose-plugin 
```
4. Устанавливаем к Docker утилиту Docker Compose:
```bash
sudo apt update
sudo apt-get install docker-compose-plugin 
```
5. В директорию проекта копируем файл `docker-compose.production.yml` и запускаем Docker Compose:
```bash
sudo docker-compose up
```
6. Создание Docker-образов. Замените username на ваш логин на DockerHub:
```bash
cd frontend
docker build -t username/kittygram_frontend .
cd ../backend
docker build -t username/kittygram_backend .
cd ../nginx
docker build -t username/kittygram_gateway . 
```
7. Загрузите образы на DockerHub:
```bash
docker push username/kittygram_frontend
docker push username/kittygram_backend
docker push username/kittygram_gateway
```
8. Деплой на сервере. Подключитесь к удаленному серверу
```bash
ssh -i путь_до_файла_с_SSH_ключом/название_файла_с_SSH_ключом имя_пользователя@ip_адрес_сервера 
```
9. Установка docker compose на сервер:
```bash
sudo apt update
sudo apt install curl
curl -fSL https://get.docker.com -o get-docker.sh
sudo sh ./get-docker.sh
sudo apt-get install docker-compose-plugin
```
10. В директорию kittygram/ скопируйте файлы docker-compose.production.yml и .env:
```bash
scp -i path_to_SSH/SSH_name docker-compose.production.yml username@server_ip:/home/username/kittygram/docker-compose.production.yml
* ath_to_SSH — путь к файлу с SSH-ключом;
* SSH_name — имя файла с SSH-ключом (без расширения);
* username — ваше имя пользователя на сервере;
* server_ip — IP вашего сервера.
```
11. Запустите docker compose в режиме демона:
```bash
sudo docker compose -f docker-compose.production.yml up -d
```
12. Для адаптации его на своем сервере добавьте секреты в GitHub Actions:
```bash
DOCKER_USERNAME                # имя пользователя в DockerHub
DOCKER_PASSWORD                # пароль пользователя в DockerHub
HOST                           # ip_address сервера
USER                           # имя пользователя
SSH_KEY                        # приватный ssh-ключ (cat ~/.ssh/id_rsa)
SSH_PASSPHRASE                 # кодовая фраза (пароль) для ssh-ключа

TELEGRAM_TO                    # id телеграм-аккаунта (можно узнать у @userinfobot, команда /start)
TELEGRAM_TOKEN                 # токен бота (получить токен можно у @BotFather, /token, имя бота)
``` 
## Примеры запросов

Добавить питомца: POST `/cats/add`

Редактировать питомца: PUTCH `/cats/edit`

Просмотр питомца: GET `/cats/{cat_id}`

## Об авторе
Python-разработчик
>[Павел Колесников](https://github.com/mrclive7406)
