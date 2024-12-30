```
class Account < Dry::Struct
	attribute :owner, User
	attribute :balance, Types::Integer.fallback(0)
end
```
fallback если неправильный тип
default если пусто