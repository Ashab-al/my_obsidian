Другое существенное свойство в объекте операций - это объект `responses`. Для свойства `responses` обычно ссылаются на полное определение в объекте `components`, поэтому рассказ об объекте `responses` в следующем разделе - [Шаг 5. Объект `components`](https://starkovden.github.io/step5-components-object.html). (На этом шаге уже слишком много информации.)

На данный момент, чтобы редактор Swagger проверил и показал наш путь, давайте просто добавим некоторый контент-заполнитель для `responses`:

```
responses:
  200:
    description: Successful response
    content:
      application/json:
        schema:
          title: Sample
          type: object
          properties:
            placeholder:
              type: string
              description: Placeholder description

  404:
    description: Not found response
    content:
      text/plain:
        schema:
          title: Weather not found
          type: string
          example: Not found
```