# dendroscan-infra
- Репозиторий по запуску сервиса dendroscan
- Сервис предназначен для анализа изображений деревьев и кустарников.
- Позволяет по фотографии находить породу растения и дефекты если они будут обнаружены.


### Сервис состоит из следующих сервисов:

- `backend`: API-сервис на порту 8000. https://github.com/potapovjakov/dendroscan-api.git
- `ml-service`: ML-сервис на порту 8080. https://github.com/potapovjakov/dendroscan-ml.git
- `db`: База данных PostgreSQL.
- `nginx`: Веб-сервер Nginx на портах 80 и 443.
- `frontend`: Фронтенд-приложение для взаимодействия с пользователем через веб-браузер. https://github.com/potapovjakov/dendroscan-frontend.git
- `minio`
И приложений:
- `dendroscan-bot`: Telegram-бот для взаимодействия с пользователем через телеграм. https://github.com/potapovjakov/dendroscan-bot.git
- `dendroscan-max-bot`: Бот для взаимодействия с пользователем через max (в разработке). https://github.com/potapovjakov/dendroscan-max-bot.git
- `dendroscan-android`: Android-приложение для взаимодействия с пользователем непосредственно со смартфона. https://github.com/potapovjakov/dendroscan-android.git


## Описание работы:
- API шлюз принимает `POST` запрос `multipart/data` по эндпоинту `/api/start`
- Отправляет запрос в `ml-service`
- Получает ответ и отдает пользователю. Пример ответа:

```json
{
  "request_id":"727ada3c-ec8c-47db-8129-aec15869faca",
  "user_id":"1",
  "scans":{
    "id":"210f9b8a-6f9f-4ce2-907e-30e53cc37d45",
    "predict":{
      "plants":[
        {
          "id":1,
          "name":"Лиственница",
          "latin_name":"Larix",
          "type":"Дерево",
          "confidence":0.4397432804107666,
          "defects":[],
          "processing_time":4.214,
          "crop_url":"https://dendroscan.s3.cloud.ru/727ada3c-ec8c-47db-8129-aec15869faca/object_0_Tree.jpg"
        },
        {
          "id":1,
          "name":"Пузыреплодник калинолистный",
          "latin_name":"Physocarpus opulifolius",
          "type":"Куст",
          "confidence":0.3454875648021698,
          "defects":[
            {
              "name":"переросший/неподрезанный куст",
              "confidence":0.2538050711154938
            },
            {
              "name":"куст с множеством сухих ветвей",
              "confidence":0.42884302139282227
            }
          ],
          "processing_time":4.085,
          "crop_url":"https://dendroscan.s3.cloud.ru/727ada3c-ec8c-47db-8129-aec15869faca/object_1_kust.jpg"
        },
        {
          "id":1,
          "name":"Ель",
          "latin_name":"Picea",
          "type":"Дерево",
          "confidence":0.47659194469451904,
          "defects":[],
          "processing_time":4.053,
          "crop_url":"https://dendroscan.s3.cloud.ru/727ada3c-ec8c-47db-8129-aec15869faca/object_2_Tree.jpg"
        },
        {
          "id":1,
          "name":"Туя",
          "latin_name":"Thuja",
          "type":"Дерево",
          "confidence":0.45147234201431274,
          "defects":[],
          "processing_time":4.23,
          "crop_url":"https://dendroscan.s3.cloud.ru/727ada3c-ec8c-47db-8129-aec15869faca/object_3_Tree.jpg"}
      ],
      "framed_url":"https://dendroscan.s3.cloud.ru/727ada3c-ec8c-47db-8129-aec15869faca/727ada3c-ec8c-47db-8129-aec15869faca_annotated.jpg"
    }
  },
  "created_at":"2025-10-02T16:41:20.693866"
}
```


## Инструкции по сборке и запуску каждого приложения будут в собственных репозиториях

## Требования
- OS Linux (Ubuntu 22.04 LTS)
- Docker
- Docker Compose
- Внешнее S3 совместимое хранилище.

## Установка
1. Скопируйте файл `.env.example`
    ```bash
    cp .env.example .env
    ```
2. Заполните файл актуальными данными
3. Склонируйте репозиторий:
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

6. После запуска сервисов вы можете проверить их статус с помощью команды:
   ```bash
   docker compose ps
   ```

7. Для остановки сервисов выполните команду:
   ```bash
   docker compose down
   ```