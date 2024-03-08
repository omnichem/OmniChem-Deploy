# OmniChem-Deploy
Репозиторий позволяющий выполнить деплой всего сервиса OmniChem на сервер.

## Подготовка нового сервера
1. Добавить ключи SSH всех разработчиков в `~/.ssh/authorized_keys` используя:
    ```bash
    nano ~/.ssh/authorized_keys

2. Установить докер в соответствии с [инструкцией](https://docs.docker.com/engine/install/ubuntu/#install-using-the-repository)
3. Добавьте пользователя в группу docker (чтобы избежать использования sudo при выполнении Docker-команд):
    ```bash
    sudo usermod -aG docker $USER
4. Последующие подключение к серверу с использованием:
   ```bash
   ssh ubuntu@<IP сервера>
   
## Клонирование репозитория
1. Клонируйте репозиторий OmniChem-Deploy(https://github.com/omnichem/OmniChem-Deploy):

   ```bash
   git clone https://github.com/omnichem/OmniChem-Deploy.git
   
2. Перейдите в папку OmniChem-Deploy:   
   ```bash
   cd OmniChem-Deploy

3. Скопируйте файл `.env.example` в `.env`:
   ```bash
   cp .env.example .env

4. Задайте переменные окружения используя:
* Редактор **nano**:
    ```bash
    nano .env
* *Написать способ копирования переменных окружения с локальной машины.*

5. Запустите приложение с использованием Docker Compose:
   ```bash
   docker compose -f docker-compose-test.yml up -d

6. Остановить контейнеры:
   ```bash
   docker compose -f docker-compose-test.yml down
   
## Развертывание новой версии
1. Подтянуть изменения с [GitHab](https://github.com/omnichem/OmniChem-Deploy) используя:
   ```bash
   git pull
   
*Написать как пересобрать контейнер.*
*Написать как удалить не нужные образы.*

## Публикация образа в Docker Hub
1. Создать Dockerfile в проекте

2. Собрать образ:
   ```bash
   docker build -t omnichem/omnichem-tg-bot:v1.0.0 .
*где omnichem - имя профиля, omnichem-tg-bot - название образа, v1.0.0 - тег образа, . - пусть.*

3. Пройти авторизацию на Docker Hub:
   ```bash
   docker login

4. Запушить образ на Docker Hub:
   ```bash
   docker push omnichem/omnichem-tg-bot:v1.0.0

## Создание дампа БД
1. Подключится к контенеру:
   ```bash
       docker exec -it <имя контейнера> sh

2. Перейти в папку `dumps`:
   ```bash
       cd dumps

3. Создать дамп БД в файл `dump_file.dump`:
   ```bash
       pg_dump -Fc -U <имя пользователя> -f dump_file.dump <имя базы данных>

4. Копирование дампа на локальную машину:
   ```bash
       scp -r ubuntu@<IP сервера>:~/OmniChem-Deploy/dumps/dump_file.dump .  

5. Копирование файла на сервер:
   ```bash
       scp ./dump_file.dump ubuntu@<IP сервера>:~/OmniChem-Deploy/dumps

6. Востановление дампа:
   ```bash
       pg_restore -Fc -d <имя базы данных> -U <имя пользователя> -W -c dump_file.dump
   
