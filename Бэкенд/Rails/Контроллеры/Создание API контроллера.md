Создание API-контроллера в Ruby on Rails отличается от создания обычного контроллера тем, что API-контроллеры обычно возвращают данные в формате JSON, а не HTML. Вот пошаговое руководство по созданию API-контроллера:

1. **Создание API-контроллера**:
   Используйте команду `rails generate controller` с опцией `--api`, чтобы создать контроллер, предназначенный для работы с API. Например:

   ```bash
   rails generate controller Api::V1::Articles --api
   ```

   Это создаст контроллер в директории `app/controllers/api/v1/articles_controller.rb`.

2. **Определение действий (методов) в контроллере**:
   Откройте созданный файл контроллера `app/controllers/api/v1/articles_controller.rb` и определите действия, которые будут выполняться при определенных запросах. Например:

   ```ruby
   module Api
     module V1
       class ArticlesController < ApplicationController
         def index
           articles = Article.all
           render json: articles
         end

         def show
           article = Article.find(params[:id])
           render json: article
         end
       end
     end
   end
   ```

3. **Создание маршрутов (routes)**:
   Определите маршруты в файле `config/routes.rb`, чтобы Rails знал, какие URL должны быть обработаны контроллером. Например:

   ```ruby
   Rails.application.routes.draw do
     namespace :api do
       namespace :v1 do
         resources :articles
       end
     end
   end
   ```

4. **Тестирование**:
   Запустите сервер Rails с помощью команды `rails server` и используйте инструменты, такие как `curl` или Postman, для тестирования вашего API. Например:

   - Для списка статей: `curl http://localhost:3000/api/v1/articles`
   - Для отображения конкретной статьи: `curl http://localhost:3000/api/v1/articles/1`

5. **Обработка ошибок и валидация**:
   Для улучшения надежности API, добавьте обработку ошибок и валидацию параметров. Например:

   ```ruby
   module Api
     module V1
       class ArticlesController < ApplicationController
         rescue_from ActiveRecord::RecordNotFound, with: :record_not_found

         def index
           articles = Article.all
           render json: articles
         end

         def show
           article = Article.find(params[:id])
           render json: article
         end

         private

         def record_not_found
           render json: { error: 'Article not found' }, status: :not_found
         end
       end
     end
   end
   ```

Это базовый пример создания API-контроллера в Rails. В реальных приложениях могут быть дополнительные сложности и требования, такие как аутентификация, ограничение доступа, использование сериализаторов и т.д.