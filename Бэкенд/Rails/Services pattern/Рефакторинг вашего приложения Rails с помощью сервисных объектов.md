#программирование
#учеба
#rails

https://www.honeybadger.io/blog/refactor-ruby-rails-service-object/
https://www.toptal.com/ruby-on-rails/rails-service-objects-tutorial - работает только с впн

Объект службы — это объект Ruby, выполняющий одно действие. Он инкапсулирует процесс в вашей предметной области или бизнес-логике.

Чтобы сохранить наш код СУХИМ (не повторяйте себя) и повторно использовать это поведение с другими объектами службы, мы можем абстрагировать метод `call`в базовый `ApplicationService`класс, от которого будет наследоваться каждый объект службы:

```
class ApplicationService
	def self.call(*args, &block)
		new(*args, &block).call
	end
end
```

С помощью этого кода мы можем провести рефакторинг `BookCreator`для наследования от `ApplicationService`:

```
# app/services/book_creator.rb
class BookCreator < ApplicationService
  def initialize(title:, description:, author_id:, genre_id:)
    @title = title
    @description = description
    @author_id = author_id
    @genre_id = genre_id
  end

  def call
    create_book
  end

  private

  def create_book
    # ...
  end
end
```


### Групповые сервисные объекты в пространствах имен

Внедрение объектов обслуживания, особенно в больших приложениях, означает, что вы вырастете с одного объекта обслуживания до десятков объектов обслуживания. Чтобы улучшить организацию кода, рекомендуется группировать общие объекты служб в пространства имен. Например, в библиотечном приложении мы бы сгруппировали все сервисы, связанные с книгами, и сгруппировали все сервисы, связанные с авторами, в отдельном пространстве имен. Наша структура папок теперь будет выглядеть так:

```
services
├── application_service.rb
└── book
├── book_creator.rb
└── book_reader.rb
```

Наши сервисные объекты будут выглядеть так:

```
# services/book/book_creator.rb
module Book
  class BookCreator < ApplicationService
  ...
  end
end
```

```
# services/twitter_manager/book_reader.rb
module Book
  class BookReader < ApplicationService
  ...
  end
end
```

Наши звонки теперь станут `Book::BookCreator.call(*args) and Book::BookReader.call(*args)`.