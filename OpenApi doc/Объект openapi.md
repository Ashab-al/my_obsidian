Введем первое свойство корневого уровня для документа спецификации: `openapi`. В объекте [openapi](https://github.com/OAI/OpenAPI-Specification/blob/master/versions/3.0.2.md#oasObject) указываем версию спецификации OpenAPI для проверки. Последняя версия 3.0.2.

```
openapi: "3.0.2"
```

Пока мы не добавим сюда дополнительную информацию, будут отображаться сообщения об ошибках и примечания, например: «No operations defined in spec!». Все в порядке - на следующем шаге мы увидим дополнительную информацию.

Версия 3.0 была выпущен 2017-07-26, а 3.0.2 - 10-08-2018 (см. [«История версий»](https://github.com/OAI/OpenAPI-Specification/blob/master/versions/3.0.2.md#appendix-a-revision-history)). Большая часть информации и примеров в Интернете, а также вспомогательные инструменты часто фокусируются только на 2.0. Даже если вы заблокированы для работы для версии 2.0, можно кодировать спецификацию в 3.0, а затем воспользоваться инструментом [APIMATIC Transformer](https://www.apimatic.io/transformer), для преобразования спецификации 3.0 в 2.0. Обратная конвертация из 2.0 в 3.0 там тоже доступна.