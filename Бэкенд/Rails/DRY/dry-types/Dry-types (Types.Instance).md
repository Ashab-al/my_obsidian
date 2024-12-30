```
class User < Dry::Struct
	attribute :name, Types::Strict::String.constrained(format: /\A\p(Alnum)+ \z/)
	attribute :age, Types::Age
	attribute :height, Types::Coercible::Float
	attribute :type?, Types::Symbol.default(:guest).enum(:guest, :admin, :investor)
	attribute :sad, Types.Instance(Range)
end
```

Types.Instance(Range) - Instance проверяет относится ли атрибут к типу Range 