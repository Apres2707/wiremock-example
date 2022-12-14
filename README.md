# wiremock-example

## Запуск
Для запуска необходимо выполнить команду

`docker-compose up -d`

## Конфигурирование
Примеры создания запросов и ответов для мок-заглушек расположены в каталоге `./stubs`
При редактирование файлов, добавлении новых или удалении старых необходимо перезапустить контейнеры, чтобы изменения вступили в силу

## Использование
Для отправки запросов на уже сконфигурированные заглушки можно воспользоваться импортом в Postman файла `./wiremock.postman_collection.json`
Файл коллекции экспортирован в формате Postman 2.1

## WireMock
WireMock - это инструмент для мока web-сервисов, предоставляемая по лицензии MIT
На самом деле, мок-сервисов есть достаточное количество, даже Postman умеет мокать. Но сегодня хотел бы рассказать именно про WireMock

Сценарии использования этой библиотеки могут для себя найти как backend-разработчики, так и frontend-разработчики и тестировщики

Здесь хотелось бы сконцентрироваться на основном функционале мока и показать только что-нибудь простое.

- Поднять wiremock можно как с использованием docker так и нативно. Я рассмотрю только вариант в контейнере, тем более, что есть официальный docker образ на docker-hub. Сразу скажу о первой фишке wiremock - он может логировать все запросы и ответы. Логирование легко отключается, но я оставлю его включённым, чтобы просто в конце показать, что оно работает.
- Настраивать можно как используя встроенный API, так и используя конфигурационные файлы. В нашем случае второй вариант кажется удобнее (файлы можно просто добавить в индекс гита и мок всегда будет сконфигурирован сразу после запуска) (+gui Есть ui-админка, но она не развивается и я ею не пользовался: https://github.com/juniorgasparotto/WiremockUI)

- Сопоставление запроса
- Формирование ответа статически, но лучше динамически! Данные можно брать из запроса, из переменных окружения, из заданных параметров, а также можно использовать разные функции типа now, randomValue и т.д.

- Проксирование запроса. Если Сервис строится, то мы можем создать шаблон с низким приоритетом, который проксирует все запросы к существующему сервису. При добавлении запроса, мы создаём под него шаблон с высоким приоритетом.
- Для нагрузочного можно устанавливать задержку ответа, некорректные ответы и т.д.
- Может имитировать коллбэки на конкретные запросы после запроса в течение настраиваемого промежутка времени
- Есть сценарии. Коротко - несколько запросов-заглушек, срабатывание которых зависит от последовательности их вызова. Для нагрузочного использовали его сценарии - выдерживает хорошую нагрузку.
- Есть другие функции, о которых можно почитать на официальном сайте.

Админка: http://127.0.0.1:8080/__admin
Логи: http://127.0.0.1:8080/__admin/requests (тут можно и с фильтрами слать запросы)

Официальный сайт: https://wiremock.org/
Статьи на хабре:
Часть 1: https://habr.com/ru/company/rostelecom/blog/679276/
Часть 2: https://habr.com/ru/company/rostelecom/blog/679330/
docker image: https://hub.docker.com/r/wiremock/wiremock
