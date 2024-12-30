```
class User < Dry::Struct
	attribute :name, Types::Strict::String.constrained(format: /\A\p(Alnum)+ \z/)
	attribute :age, Types::Age
	attribute :height, Types::Coercible::Float
	attribute :type?, Types::Symbol.default(:guest).enum(:guest, :admin, :investor)
end
```

type? - сам знак ? в атрибуте говорит что можно вообще не передавать type 
ничего не будет

.enum(:guest, :admin, :investor) - говорит что допустимы только такие символы