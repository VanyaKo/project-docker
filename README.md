# Как использовать с `compose.yaml`
1. Создать в директории проекта файл `secrets.txt` и вписать туда пароль от бд
2. Запустить `docker compose up --build`
3. Помните, что `volume` постоянный. Это значит, что если хотите поменять пароль от бд или ее сбросить, уберите в `compose.yaml` все, что связано с `volumes`

# Как использовать без `compose.yaml`
Сначала устанавливаем образ [postgres](https://hub.docker.com/_/postgres) и запускаем контейнер. Затем в `Dockerfile` раскоментируйте строки

В папке проекта вводим следующие команды:
1. `docker build -f Dockerfile -t <ИМЯ_ОБРАЗА> .`
2. `docker network create <ИМЯ_BRIDGE_СЕТИ>`
4. `docker run -e POSTGRES_PASSWORD=<ПАРОЛЬ> -e POSTGRES_USER=<ЛОГИН> -d --name postgres --network <ИМЯ_BRIDGE_СЕТИ> <ИМЯ_POSTGRES_КОНТЕЙНЕРА>`
5. `docker run --name <ИМЯ_ОБРАЗА> --network <ИМЯ_BRIDGE_СЕТИ> -p <ПОРТ>:8080 web`
   Проверяем, что приложение по адресу `localhost:<ПОРТ>` работает.

Пример команд:
1. `docker build -f Dockerfile -t web .`
2. `docker network create practice-net`
3. `docker run -e POSTGRES_PASSWORD=pass -e POSTGRES_USER=postgres -d --name postgres --network practice-net postgres`
4. `docker run --name web --network practice-net -p 8080:8080 web`

Проверяем `localhost:8080`.
