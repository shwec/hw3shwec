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
При остановке redis:
healthz — 200
readyz — 503
increment — 503
после запуска redis readyz вернул 200, счётчик сохранился и увеличился до 4. контейнер приложения не перезапускался