#Тестовое задание

Проверено под docker-desktop

Запускать через docker-compose up, ничего кроме делать не надо

в hosts добавить следующее

```hosts
127.0.0.1 pma
127.0.0.1 mailtrap
127.0.0.1 test.local
```

Доступ в контейнер php для установки laravel через composer с помощью sh

```sh
docker exec -it test_php sh
```

После запуска контейнера в директории /var/www контейнера php все удалить, в том числе файл .gitkeep и только потом чистить

Цель

1. Развернуть laravel внутри контейнера `test_php` предварительно удалив все из директории `/var/www`
1. Сделать [миграцию](https://laravel.com/docs/9.x/migrations) для почтовых сообщений. Нужны поля `email`, `subject`, `text`
1. Сделать [модель](https://laravel.com/docs/9.x/eloquent) под миграцию, описав свойства в phpdoc
1. Сделать два [контроллера](https://laravel.com/docs/9.x/controllers#main-content) `RecipientController` и `MessageController`
    - У `RecipientController` нужен только метод `list` который будет возвращать уникальные `email` из таблицы почтовых сообщений
    - У `MessageController` нужен метод list с слагом `{email}` для получения списка сообщений отправленных на `email` и метод `add` для добавления сообщения, для метода `add` нужен [валидатор](https://laravel.com/docs/9.x/validation#manually-creating-validators) или [кастомный реквест](https://laravel.com/docs/9.x/validation#creating-form-requests)
1. Сделать [вьюшки](https://laravel.com/docs/9.x/views#main-content) по необходимости используя [blade-ы](https://laravel.com/docs/9.x/blade)
Общие элементы для каждой страницы: ссылка добавить и ссылка домой
    - Главная страница - список email-ов
    - Список сообщений для email
    - Форма для нового сообщения
1. Сделать отправку почты по событию создания нового письма. `to` брать из поля `email` модели почтовых сообщений, `subject` и `text` соответственно оттуда же
1. В качестве почтового сервера использовать mailtrap который уже есть в этом композере