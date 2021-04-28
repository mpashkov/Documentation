---
description: >-
  В документе описывают общение принципы которых придерживаются API разных
  продуктов Retail Rocket
---

# Общие принципы интеграции с Retail Rocket

## Основные принцыпы

Все API Retail Rocket доступны по протоколу HTTP/2 и разрабатываются придерживаясь принцыпам RESTful. 

Если для вызова метода требуется передача данных в теле запрос, то система ожидает их в формате JSON и соответствующий http-заголовок `content-type: application json`

Все данные которые возвращаются в результате вызова, возвращаются в формате JSON.  
  
Статусы HTTP-ответа имеет значение,  возможные статусы метода описываются в его документации.

## **Идентификатор интернет магазина**

Для идентификации интернет магазина с каждый вызовами требуется передать параметр `partnerId`.Значение параметра выдается при регистрации в системе Retail Rocket и может быть полученно: запросом к аккаунт менеджеру Retail Rocket, обращением в службу поддержки\(support@retailrocket.ru\) или в [личном кабинете Retail Rocket](https://my.retailrocket.ru).

{% hint style="info" %}
Значение является **публичным** и может быть использованно в открытом виде.
{% endhint %}

## Авторизация

Доступ к некоторым методам API ограничен и для их использования требуется передавать пареметр `apiKey`, значение которого получается у сотрудника Retail Rocket.

{% hint style="danger" %}
Значение `apiKey` является **секретным** и не должно передавать третьим лицам. 
{% endhint %}

{% hint style="danger" %}
С целью сохранения значения в тайне оно **не** может использоваться в мобильном приложение или на сайте интернет магазина.
{% endhint %}

{% hint style="warning" %}
В случае утечки значения `apiKey`следует запросить у аккаунт менеджера новое. Старое значение перестанет действовать.
{% endhint %}

{% hint style="info" %}
**Рекомендация**

Хранить значение `apiKey` в хранилище в котором его можно изменить без необходимости выпускать новую версию сайта/приложения.
{% endhint %}

## **Управление сессией**

Для некоторых вызовов API требуется идентифицировать посетителя между разнесенными во времени вызовами. Для этого при вызове их вызове требуется передавать идентификатор пользовательской сессии в параметре `sessionExternalId.` Идентификатор должен быть сгенерирован на стороне магазина и обладать следующими свойствами:

* Состоять только из цифр и букв;
* Не превышать 50 символов;
* Быть уникаленым для устройства/браузера;
* Не содержит персональных данных: телефона, адреса электронной почти;
* Не должен изменяться при авторизации или смене аккаунта.

{% hint style="info" %}
**Рекомендация**

При первом появление посетителя на сайте или в мобильном приложении, генерировать GUID и испльзовать его в качестве `sessionExternalId` для последующих вызовав API.
{% endhint %}

## Временная метка вызова

Для корректной работы многих продуктов Retail Rocket необходимо знать время когда метод был вызван,  для этого некоторые API методы предусмоторен опциональный параметр `timestamp`, в значение которого система Retail Rocket ожидает дату и время в формате ISO 8601. 

Если опциональный параметр не задан, то будет использованно серверное время Retail Rocket на момент вызова в качестве временной метки.

## Сведения о товаре

Если в методе API требуются товарные данные, например: идентификатор товара/склада и т.д.. Значение товарных параметров должно совпадать с значениями переданных с товарной базой в Retail Rocket\(в yml файле\).


