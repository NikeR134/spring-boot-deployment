# Spring Boot deployment

Учебный Spring Boot проект для практики создания Docker-образа, запуска сервиса через systemd и настройки Nginx как обратного прокси.

Перед сборкой требуется JDK 21 и Maven. Инструкции и конфигурационные файлы находятся в `deploy/`.

Локальная проверка приложения:

```bash
mvn clean package
docker compose -f deploy/docker-compose.yml up --build -d
curl http://localhost:8080/health
```

