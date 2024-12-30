# one-to-one

class Profile
  belongs_to :user
end

class User
  has_one :profile
end
 
**Миграция**
class CreateUsers < ActiveRecord::Migration[7.0]
  def change
    create_table :users do |t|
      t.string :username
      t.string :emailt
      t.timestamps
    end
  end
end

class CreateProfiles < ActiveRecord::Migration[7.0]
  def change
    create_table :profiles do |t|
      t.references :user, null: false, foreign_key: true
      t.timestamps
    end
  end
end

# SQL

CREATE TABLE user (
  id SERIAL PRIMARY KEY,
  username VARCHAR(50) NOT NULL
);

CREATE TABLE profiles (
  id SERIAL PRIMARY KEY,
  user_id INTEGER UNIQUE,
  FOREIGN KEY (user_id) REFERENCES users(id)
);

# one-to-many
class Post
  belongs_to :user
end

class User
  has_many :posts
end

**Миграция**
class CreateUsers < ActiveRecord::Migration[7.0]
  def change
    create_table :users do |t|
      t.string :username
      t.string :email
      t.timestamps
    end
  end
end

class CreatePosts < ActiveRecord::Migration[7.0]
  def change
    create_table :posts do |t|
      t.references :user, null: false, foreign_key: true
      t.string :title
      t.text :content
      t.timestamps
    end
  end
end

# SQL
CREATE TABLE user (
  id SERIAL PRIMARY KEY,
  username VARCHAR(50) NOT NULL
);

CREATE TABLE posts (
  id SERIAL PRIMARY KEY,
  title VARCHAR(100),
  content TEXT,
  user_id INTEGER UNIQUE,
  FOREIGN KEY (user_id) REFERENCES users(id)
);

# many-to-many

class Product
  has_and_belongs_to_many :categories
end

class Category
  has_and_belongs_to_many :products
end

**Миграции**
class CreateProducts < ActiveRecord::Migration[7.0]
  def change
    create_table :products do |t|
      # Добавьте нужные столбцы в таблицу products
      t.string :name
      t.text :description
      t.decimal :price, precision: 8, scale: 2
      # Добавьте другие столбцы, если это необходимо
      t.timestamps
    end
  end
end

class CreateCategories < ActiveRecord::Migration[7.0]
  def change
    create_table :categories do |t|
      # Добавьте нужные столбцы в таблицу categories
      t.string :name
      t.text :description
      # Добавьте другие столбцы, если это необходимо
      t.timestamps
    end
  end
end

class CreateJoinTableProductCategory < ActiveRecord::Migration[7.0]
  def change
    create_join_table :products, :categories do |t|
      # t.index [:product_id, :category_id]
      # t.index [:category_id, :product_id]
    end
  end
end
# SQL
CREATE TABLE products (
  id SERIAL PRIMARY KEY,
  title VARCHAR(100) NOT NULL
);

CREATE TABLE categories (
  id SERIAL PRIMARY KEY,
  name VARCHAR(100) NOT NULL
);

CREATE TABLE product_categories (
  product_id INTEGER,
  category_id INTEGER,
  PRIMARY KEY (product_id, category_id),
  FOREING_KEY (product_id) REFERENCES products(id),
  FOREING_KEY (category_id) REFERENCES categories(id)
);

# through
class User
  has_many :user_events
  has_many :events, through: :user_events
end

class Event
  has_many :user_events
  has_many :users, through: :user_events
end

class UserEvent
  belongs_to :user
  belongs_to :event
end

**Миграция**
class CreateUsers < ActiveRecord::Migration[7.0]
  def change
    create_table :users do |t|
      # Добавьте нужные столбцы в таблицу users
      t.string :username
      t.string :email
      t.string :password_digest
      # Добавьте другие столбцы, если это необходимо
      t.timestamps
    end
  end
end

class CreateEvents < ActiveRecord::Migration[7.0]
  def change
    create_table :events do |t|
      # Добавьте нужные столбцы в таблицу events
      t.string :title
      t.text :description
      t.datetime :event_date
      # Добавьте другие столбцы, если это необходимо
      t.timestamps
    end
  end
end

class CreateUserEvents < ActiveRecord::Migration[7.0]
  def change
    create_table :user_events do |t|
      t.references :user, null: false, foreign_key: true
      t.references :event, null: false, foreign_key: true
      t.timestamps
    end
  end
end
# Indexs
#
# Ускроение поиска данных
# Но расходует больше памяти

# INNER JOIN
# оператор внутреннего соединения (2 таблицы). Выбирает совпадения
# из объединяемых таблицы
#
# OUTER JOIN
# LEFT
# указывает что внешней таблицей будет ноходящяяся слева
# RIGHT
# указывает что внешней таблицей будет ноходящяяся справа
# берутся все данные из внешней таблицы + совпадения из второй
#
# Full join
# возвращает объединение LEFT и RIGHT таблиц, но комбинирует
# результат этих запрсов
#
# Cross join
# перекрестное объединение
# выборка записей первой таблицы объединенная с каждой строкой второй
#
# Indexs
#
# B-three
# SQL
# CREATE INDEX idx_email ON users (email);
#
# migration
class AddIntexToUsersEmail < ActiveRecord::Migration[6.6.6]
  def change
    add_index :users, :email
  end
end

# Hash indexes
# SQL
# CREATE INDEX idx_user_id ON users USING HASH (user_id)
# migration
class AddIntexToUsersEmail < ActiveRecord::Migration[6.6.6]
  def change
    add_index :users, :email, using: 'hash'
  end
end

# Full-text
# SQL
# CREATE FULLTEXT INDEX idx_description ON products (description)
  def change
    execute "CREATE FULLTEXT INDEX idx_description ON products (description)"
  end

class AddFullTextIndexToPostsContent
   def change
     execute "CREATE INDEX idx_posts_content On posts USING GIN(to_tsvecor('english'))"
   end
end
