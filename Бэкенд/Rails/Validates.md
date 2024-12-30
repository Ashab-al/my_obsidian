- [`:allow_nil`](https://edgeguides.rubyonrails.org/active_record_validations.html#allow-nil): Пропустить проверку, если атрибут имеет значение `nil`.
- [`:allow_blank`](https://edgeguides.rubyonrails.org/active_record_validations.html#allow-blank): Пропустить проверку, если атрибут пуст.
- [`:message`](https://edgeguides.rubyonrails.org/active_record_validations.html#message): укажите собственное сообщение об ошибке.
- [`:on`](https://edgeguides.rubyonrails.org/active_record_validations.html#on): укажите контексты, в которых эта проверка активна.
- [`:strict`](https://edgeguides.rubyonrails.org/active_record_validations.html#strict-validations): вызвать исключение в случае сбоя проверки.
- [`:if`и`:unless`](https://edgeguides.rubyonrails.org/active_record_validations.html#conditional-validation) : укажите, когда должна или не должна выполняться проверка.

### [3.2`:allow_blank`](https://edgeguides.rubyonrails.org/active_record_validations.html#allow-blank)

Вариант `:allow_blank`аналогичен варианту `:allow_nil`. Эта опция позволит пройти проверку, если значение атрибута равно `blank?`, например `nil`, или пустой строке.

```
class Topic < ApplicationRecord
  validates :title, length: { is: 5 }, allow_blank: true
end
```

### [3.1`:allow_nil`](https://edgeguides.rubyonrails.org/active_record_validations.html#allow-nil)

Эта `:allow_nil`опция пропускает проверку, если проверяемое значение равно `nil`.

```
class Coffee < ApplicationRecord
  validates :size, inclusion: { in: %w(small medium large),
    message: "%{value} is not a valid size" }, allow_nil: true
end
```