# dendroscan-infra
Репозиторий по запуску сервиса dendroscan
Сервис предназначен для анализа изображений деревьев и кустарников.
Позволяет по фотографии находить породу растения и дефекты если они будут обнаружены.

Сервис состоит из следующих сервисов:



https://github.com/potapovjakov/dendroscan-infra.git





- `backend`: API-сервис на порту 8000. https://github.com/potapovjakov/dendroscan-api.git
- `ml-service`: ML-сервис на порту 8080. https://github.com/potapovjakov/dendroscan-ml.git
- `db`: База данных PostgreSQL.
- `nginx`: Веб-сервер Nginx на портах 80 и 443.
- `frontend`: Фронтенд-приложение для взаимодействия с пользователем через веб-браузер. https://github.com/potapovjakov/dendroscan-frontend.git

И приложений:
- `dendroscan-bot`: Telegram-бот для взаимодействия с пользователем через телеграм. https://github.com/potapovjakov/dendroscan-bot.git
- `dendroscan-max-bot`: Бот для взаимодействия с пользователем через max (в разработке). https://github.com/potapovjakov/dendroscan-max-bot.git
- `dendroscan-android`: Android-приложение для взаимодействия с пользователем непосредственно со смартфона. https://github.com/potapovjakov/dendroscan-android.git

## Требования
- OS Linux (Ubuntu 22.04 LTS)
- Docker
- Docker Compose

## Установка

1. Склонируйте репозиторий:
   ```bash
   git clone https://github.com/dendroscan/dendroscan-infra.git
   ```
## Инструкция по запуску сервиса

Для запуска сервиса из репозитория `dendroscan-infra` выполните следующие шаги:
1. Убедитесь, что на вашем компьютере установлен Docker и Docker Compose.
2. Склонируйте данный репозиторий на свой компьютер.
3. Перейдите в корневую директорию репозитория `dendroscan-infra`.
4. Выполните команду для загрузки Docker образов из репозитория DockerHub:
   ```bash
   docker compose pull
   ```
5. Выполните команду для запуска всех сервисов, описанных в файле `docker-compose.yml`:

   ```bash
   docker compose up -d
   ```
   Эта команда запустит следующие сервисы:
   - `backend`: API-сервис на порту 8000.
   - `ml-service`: ML-сервис на порту 8080.
   - `db`: База данных PostgreSQL.
   - `nginx`: Веб-сервер Nginx на портах 80 и 443.
   - `frontend`: Фронтенд-приложение.

5. После запуска сервисов вы можете проверить их статус с помощью команды:
   ```bash
   docker compose ps
   ```

6. Для остановки сервисов выполните команду:
   ```bash
   docker compose down
   ```
   