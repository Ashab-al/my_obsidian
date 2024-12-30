```
class Account < Dry::Struct
	attribute :owner, User
	attribute :balance, Types::Integer.fallback(0)
	attribute :description, Types::Strict::String.optional
end
```

.optional -  атрибут может быть nil но если он не nil то обязательно должна быть проверка Types::Strict::String