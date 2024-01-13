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
   docker compose up -d
   
## Развертывание новой версии
1. Подтянуть изменения с [GitHab](https://github.com/omnichem/OmniChem-Deploy) используя:
   ```bash
   git pull
   
*Написать как пересобрать контейнер.*
*Написать как удалить не нужные образы.*

   