#программирование 
#ruby 
#dry
```
user_hash = Types::Hash.schema(
	name: Types::Strict::String,
	age: Types::Strict::Integer.
		  default(18).
		  constructor { |value|
			  value.nil? ? Dry::Types::Undefined : value
		  }
).strict.with_key_transform(&:to_sym)

p user_hash["name": 'asdasd', "age":nil]
```

).strict.with_key_transform(&:to_sym)

strict не дает передавать лишние ключи
Если передать user_hash["name": 'asdasd', "age":nil, test:nil]
То выведет ошибку что нет ключа test в схеме

А .with_key_transform(&:to_sym) переделывает все ключи в символы