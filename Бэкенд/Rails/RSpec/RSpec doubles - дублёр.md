doubles - дублёр.
Виды дублёров:
  1. stub - детерминировано работа методов и возвращение значений (proc)
  2. mock - обязателен вызов метода (lambda)
  3. null object - returned self
  4. spy == stub, "некоторые логи"


Пример теста используя дублер
```
context 'when performing money withdrawal' do
	before { allen.deposit 300 }

	specify "#transfer_with_conversation" do

		allow(allen).to receive(:convert).
		  with(sum: 100, from: :usd, to: :eur).
		  and_return(80)

		allen.transfer_with_conversation kirill, 100, :usd, :eur

		expect(allen.balance).to eq(200)
		expect(kirill.balance).to eq(80)
		expect(allen).to have_received(:convert).once
	end
end
```

И еще один пример

```
RSpec.describe Exchanger::Api::Converter do
	specify "#convert" do
		converter_stub = instance_double 'Exchanger::Api::Converter'
		
		allow(converter_stub).to receive(:convert).with(sum: 100).and_return(50)
		
		expect(converter_stub.convert(sum: 100)).to eq(50)
		
		expect(converter_stub).to have_received(:convert).with(sum: 100).once
	end
end
```