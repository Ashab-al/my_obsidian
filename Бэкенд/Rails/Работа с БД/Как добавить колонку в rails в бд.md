Чтобы добавить колонку в базу данных в Ruby on Rails, нужно выполнить несколько шагов:

1. Сгенерировать миграцию, используя команду `rails generate migration` с указанием имени миграции и имени колонки.

2. Отредактировать созданную миграцию, добавив код для добавления колонки в метод `change` или `up`.

3. Запустить миграцию, чтобы применить изменения к базе данных.

Вот пример шагов для добавления колонки с именем `new_column` в таблицу `example_table`:

1. Генерация миграции:

```bash
rails generate migration AddNewColumnToExampleTable new_column:string

или

rails generate migration add_email_to_users email:string
```

Здесь `AddNewColumnToExampleTable` - это имя миграции, а `new_column:string` указывает, что мы добавляем колонку `new_column` с типом данных `string`.

2. Редактирование миграции:

Откройте созданную миграцию, расположенную в директории `db/migrate`, и внесите изменения в метод `change` или `up`, чтобы добавить новую колонку. Пример:

```ruby
class AddNewColumnToExampleTable < ActiveRecord::Migration[6.0]
  def change
    add_column :example_table, :new_column, :string
  end
end
```

3. Запуск миграции:

Выполните команду `rails db:migrate` для применения изменений к базе данных:

```bash
rails db:migrate
```

Это применит миграцию и добавит новую колонку в таблицу `example_table` в базе данных.