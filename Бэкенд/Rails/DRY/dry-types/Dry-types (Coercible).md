#программирование 
#ruby 
#dry
```
module Types
	include Dry.Types()
	Age = Integer.constrained(gteq: 0)
end

class Character < Dry::Struct
	attribute :name, Types::Strict::String
	attribute :age, Types::Age
	attribute :height, Types::Coercible::Float
end

alln = Character.new name: 'Allen', age: 100, height: '120.1'
```

Types::Coercible::Float
Coercible - переводит к указанному типу данные
если придет '120.1' из него сделает 120.1
если придет 'asd' то выведет ошибку 