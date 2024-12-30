В объекте `servers` указывается базовый путь, используемый в ваших запросах API. Базовый путь - это часть URL, которая находится перед конечной точкой.

## Пример объекта `servers`[](https://starkovden.github.io/step3-servers-object.html#%D0%BF%D1%80%D0%B8%D0%BC%D0%B5%D1%80-%D0%BE%D0%B1%D1%8A%D0%B5%D0%BA%D1%82%D0%B0-servers)

Пример объекта `servers`

```
servers:
- url: https://api.openweathermap.org/data/2.5/
```

Каждая из конечных точек (называемых в спецификации `paths`) будет добавляться ​​к URL-адресу сервера, при отправке пользователями пробных запросов `Try it out`. Например, если одним из путей является `/weather`, то при отправке запроса Swagger UI представит путь к `{server URL}{path}` или [https://api.openweathermap.org/data/2.5/weather](https://api.openweathermap.org/data/2.5/weather).

## Опции URL сервера[](https://starkovden.github.io/step3-servers-object.html#%D0%BE%D0%BF%D1%86%D0%B8%D0%B8-url-%D1%81%D0%B5%D1%80%D0%B2%D0%B5%D1%80%D0%B0)

Объект `servers` обладает гибкой настройкой. Можно указать несколько URL-адресов серверов, которые могут относиться к различным средам (тестовая, бета-версия, рабочая версия). При наличии нескольких URL-адресов серверов, пользователи могут выбирать среду в раскрывающемся списке серверов. Можно указать несколько URL-адресов серверов, например:

```
servers:
  - url: https://api.openweathermap.org/data/2.5/
        description: Production server
  - url: http://beta.api.openweathermap.org/data/2.5/
        description: Beta server
  - url: http://some-other.api.openweathermap.org/data/2.5/
        description: Some other server
```

