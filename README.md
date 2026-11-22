сделал на 8 баллов
запуск
docker compose up -d --build

проверка
curl localhost:8888
curl -X POST localhost:8888/increment

остановка
docker compose down


PORT — порт, дефолтное значение 8888.
GREETING — приветствие, дефолтное hi.
Хранилище — redis с постоянным volume

проверка
SQLite: счётчик сохранился после пересоздания контейнера
redis: после пересоздания контейнеров count остался равен 3.
команды
docker compose down
docker compose up -d
curl localhost:8888
При отключении redis:
docker compose stop redis
curl -i localhost:8888/healthz
curl -i localhost:8888/readyz
curl -i -X POST localhost:8888/increment

получилось:

healthz — 200
readyz — 503
increment — 503


восстановление
docker compose start redis
curl -i localhost:8888/readyz
curl localhost:8888
curl -X POST localhost:8888/increment


после запуска redis readyz вернул 200, счётчик сохранился и увеличился до 4. контейнер приложения не перезапускался