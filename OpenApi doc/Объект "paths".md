## Объекты `paths`[](https://starkovden.github.io/step4-paths-object.html#%D0%BE%D0%B1%D1%8A%D0%B5%D0%BA%D1%82%D1%8B-paths)

 **Note:** Объект `paths` - это та же «конечная точка» в соответствии с терминологии спецификации OpenAPI.

Каждый элемент в объекте `path` содержит [объект `operations`](https://github.com/OAI/OpenAPI-Specification/blob/master/versions/3.0.2.md#operation-object). (`operations` - это методы GET, POST, PUT и DELETE, которые мы изучали в разделе [Конечные точки](https://starkovden.github.io/step2-endpoints-and-methods.html) руководства по API.)

Начинаем с перечисления путей (конечных точек) и их разрешенных операций (методов). Для конечной точки `weather` в API OpenWeatherMap есть только один путь (`/weather`) и одна операция (`get`) для этого пути:

```
paths:
  /weather:
    get:
```

### Объект `operations`[](https://starkovden.github.io/step4-paths-object.html#%D0%BE%D0%B1%D1%8A%D0%B5%D0%BA%D1%82-operations)

Объект операции ( `get` приведенный выше в коде) содержит различные свойства и объекты:

- `tags`: групповое имя для организации путей в интерфейсе Swagger. Swagger UI сгруппирует конечные точки под заголовками тегов.
- `summary`: краткое описание пути. Swagger UI показывает описание рядом с именем пути. Ограничивают описание только 5-10 словами. Описание отображается и при свернутом разделе.
- `description`: Полное описание пути. Может содержать неограниченное количество деталей. В Swagger UI достаточно места для полного описания. CommonMark Markdown разрешен.
- [`externalDocs`](https://github.com/OAI/OpenAPI-Specification/blob/master/versions/3.0.2.md#externalDocumentationObject) (объект): ссылка на документацию с доп. информацией о пути.
- `operationId`: уникальный идентификатор пути.
- [`parameters`](https://github.com/OAI/OpenAPI-Specification/blob/master/versions/3.0.2.md#parameterObject) (объект): Параметры, принимаемые путем. Не включает параметры тела запроса, которые подробно описаны в объекте `requestBody`. Объект `parameters` также может включать в себя [объект `reference`](https://github.com/OAI/OpenAPI-Specification/blob/master/versions/3.0.2.md#referenceObject), который содержит указатель на описание в объекте `components` (этот объект описан на [шаге 5: Объект `components`](https://starkovden.github.io/step5-components-object.html) ).
- [`requestBody`](https://github.com/OAI/OpenAPI-Specification/blob/master/versions/3.0.2.md#requestBodyObject) (объект): детали параметра тела запроса для этого пути. Объект `requestBody` также может включать в себя [объект `reference`](https://github.com/OAI/OpenAPI-Specification/blob/master/versions/3.0.2.md#referenceObject), который содержит указатель на описание в объекте `components` (описание в [шаге 5: Объект `components`](https://starkovden.github.io/step5-components-object.html) ).
- [`response`](https://github.com/OAI/OpenAPI-Specification/blob/master/versions/3.0.2.md#responsesObject) (объект): ответы, предоставленные на запросы по этому пути. Объект `response` также может включать в себя [объект `reference`](https://github.com/OAI/OpenAPI-Specification/blob/master/versions/3.0.2.md#referenceObject), который содержит указатель на описание в объекте `components`. Ответы используют стандартные [коды состояния](https://github.com/OAI/OpenAPI-Specification/blob/master/versions/3.0.2.md#http-status-codes).
- [`callbacks`](https://github.com/OAI/OpenAPI-Specification/blob/master/versions/3.0.2.md#callbackObject) (объект): детали обратного вызова могут быть инициированы сервером при желании. Callbacks - это операции, выполняемые после завершения выполнения функции. Объект `callbacks` также может включать в себя [объект `reference`](https://github.com/OAI/OpenAPI-Specification/blob/master/versions/3.0.2.md#referenceObject), который содержит указатель на описание в объекте `components`.
- `deprecated`: Является ли путь устаревшим. Можно опустить, если вы не хотите указать устаревшее поле. Boolean.
- [`security`](https://github.com/OAI/OpenAPI-Specification/blob/master/versions/3.0.2.md#securityRequirementObject) (объект): Метод безопасной авторизации, используемый с операцией. Этот объект добавляется на уровне пути, только если нужно перезаписать объект `security` на корневом уровне. Имя определяется объектом `securitySchemes` в объекте `components`. Более подробная информация об этом представлена ​​в [шаге 6: объект `security`](https://starkovden.github.io/step6-security-object.html).
- [`servers`](https://github.com/OAI/OpenAPI-Specification/blob/master/versions/3.0.2.md#serverObject) (объект): Объект `servers`, который может отличаться от [глобального объекта `servers`](https://starkovden.github.io/step3-servers-object.html) для этого пути.

Каждое из вышеупомянутых свойств, имеющих гиперссылку и «(объект)», содержат дополнительные уровни. Их значения не просто типы данных, такие как строки, а скорее объекты, которые содержат свои собственные свойства.

 **Tip:** Несомненно, нужно обращаться к [спецификации OpenAPI](https://github.com/OAI/OpenAPI-Specification/blob/master/versions/3.0.2.md), чтобы узнать, какие детали требуются для каждого из значений и объектов. На курсе нет возможности воспроизвести все нужные детали. Здесь просто поверхностное знакомство со свойствами OpenAPI.

Давайте добавим скелет объекта `operations` к нашему коду:

```
paths:
  /weather:
    get:
      tags:
      summary:
      description:
      operationId:
      externalDocs:
      parameters:
      responses:
      deprecated:
      security:
      servers:
      requestBody:
      callbacks:
```

И удалим несколько ненужных полей, которые нам не нужны для нашей документации по API OpenWeatherMap:

- Нет необходимости включать [объект `requestBody`](https://github.com/OAI/OpenAPI-Specification/blob/master/versions/3.0.2.md#requestBodyObject) потому что ни один путь API OpenWeatherMap не содержит параметров тела запроса.
- Нет необходимости включать [объект `servers`](https://github.com/OAI/OpenAPI-Specification/blob/master/versions/3.0.2.md#serverObject) потому что используется тот же URL глобальных `servers`, который мы определили [глобально на корневом уровне](https://starkovden.github.io/step3-servers-object.html)
- Нет необходимости включать [security](https://github.com/OAI/OpenAPI-Specification/blob/master/versions/3.0.2.md#securityRequirementObject) потому что используется один и тот же объект `security`, который мы определим глобально на корневом уровне позже (см. [Шаг 6: объект `security`](https://starkovden.github.io/step6-security-object.html) ).
- Нет необходимости включать `deprecated` потому что ни один из путей не устарел.
- Нет необходимости включать `callbacks` потому что ни один из путей не использует колбэки.

В результате мы можем уменьшить количество соответствующих полей до следующего:

```
paths:
  /weather:
    get:
      tags:
      summary:
      description:
      operationId:
      externalDocs:
      parameters:
      responses:
```

Большинство свойств для объектов операции либо требуют простых строк, либо содержат относительно простые объекты. Наиболее подробные объекты здесь - это [объект `parameters`](https://starkovden.github.io/step4-paths-object.html#parameters) и [объект `responses`](https://starkovden.github.io/step4-paths-object.html#responses).