# Как использовать
В папке проекта вводим следующие команды:
1. `docker build -f Dockerfile -t web .`
2. `docker network create practice-net`
3. `docker run -e POSTGRES_PASSWORD=pass -e POSTGRES_USER=postgres -d --name postgres --network practice-net postgres`
4. `docker run --name web --network practice-net -p 8080:8080 web`

Проверяем, что приложение по адресу `localhost:8080` работает.
