# Развёртывание

Соберите JAR-файл и Docker-образ:

```bash
mvn clean package
docker compose -f deploy/docker-compose.yml build
```

Для переноса образа на сервер сохраните его в архив, передайте через SCP и загрузите на сервере:

```bash
docker save myapp:latest -o myapp.tar
scp myapp.tar user@your-server:/tmp/myapp.tar
ssh user@your-server docker load -i /tmp/myapp.tar
```

Для локального запуска через Compose:

```bash
docker compose -f deploy/docker-compose.yml up -d
curl http://localhost:8080/health
```

Для запуска через systemd установите Docker на сервере и скопируйте `myapp.service` в `/etc/systemd/system/`:

```bash
sudo systemctl daemon-reload
sudo systemctl enable --now myapp.service
sudo systemctl status myapp.service
```

Скопируйте `nginx.conf` в `/etc/nginx/conf.d/myapp.conf`, проверьте конфигурацию и перезагрузите Nginx:

```bash
sudo nginx -t
sudo systemctl reload nginx
sudo ufw allow 80/tcp
```

Проверьте приложение и журналы:

```bash
curl http://localhost/health
sudo journalctl -u myapp.service -f
sudo tail -f /var/log/nginx/access.log
```

