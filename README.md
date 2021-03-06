# Order Management System - SPA

# Запуск
Для запуска нужно развернуть `dist.zip` на web-сервере в корень (например `http://localhost/`, а не 
`http://localhost/dist/`). По-умолчанию клиент считает, что API расположен на `http://localhost:8080`. Чтобы изменить 
эти данные, нужно отредактировать исходный файл `src/env.js` и собрать приложение заново с помощью команд `npm install` 
и `npm run build` (для сборки необходим npm),

## Описание клиента
Знакомство с приложением начинается с авторизации. Если пользователь еще не зарегистрирован, он может сделать это,
придумав уникальное имя пользователя, пароль и выбрав типа пользователя - исполнитель или заказчик. От этого выбора 
будут зависеть возможности, предоставляемые приложением.

После авторизации заказчикам доступна лишь одна вкладка - "Мои заказы". В этой вкладке он может создать новый заказ, 
нажав на большую красную кнопку внизу экрана. После того как заказчик введет данные и нажмет [Создать], белая карточка 
с этим заказом появится в списке заказов заказчика, а также она будет доступна исполнителям в спсике "Новые заказы". Во 
вкладке "Мои заказы" заказчик может контролировать статус своих заказов и оплачивать свои заказы, ожидающие 
подтверждения.

Исполнителям доступно две вкладки - "Новые заказы" и "Мои заказы". В первой вкладке отображаются заказы, которые были 
опубликованы заказчиками, но которые никто еще не взялся выполнять. карточки таких заказов белого цвета (подробнее о 
цветах карточек будет описано ниже). Исполнитель может взять любой из таких заказов, нажав на кнопку [Взять]. Заказ 
появится в списке "Мои заказы" и исчезнет из списка новых заказов (в т.ч. и для других пользователей). Во вкладке "Мои 
заказы" исполнитель может контролировать статус заказов, исполнителем которых он является, и отправлять заказы на 
подтверждение заказчику.

### Цвета карточек и статусы заказов
Цвет|Статус
----|------
Белый|[WAITING](../../../rest-api#waiting)
Голубой|[IN PROGRESS](../../../rest-api#in-progress)
Желтый|[READY](../../../rest-api#ready)
Зеленый|[COMPLETED](../../../rest-api#completed)
