TDD - Test Driven development

1. test
2. code
3. run tests
4. refactoring
5. run tests

Test first. repeat(test -> code -> test)
a) isolate - mock, stub. Тест не зависит от другого теста. Rspec - order random
b) usable - покрытие всех случаев использование
c) validatable - корректность валидаций
d) references - зависимости между моделями
e) rubocop - читабельно, понятно
f) auto - bin/dev - test first -> application -> production (deployment)

BDD - Behavior Driven development
любое поведение системы

1. Определить поведние (user stories)
Feature: Добавление нового курса
  Scenario: Пользователь добавляет новый курс
    Given: пользователь находится на странице добавления курса
    When: пользователь вводит название "Python course" и описание "about python in 20 lesson"
    AND: пользователь жмёт кнопку "Create"
    Then: Должен создаться курс в системе с названием "Python course"

# Gemfile
gem 'rspec'
gem 'rspec-rails'
gem 'capybara'

# spec/features/add_course_spec.rb
require 'rails_helper'

RSpec.feature "Add Course", type: :feature do
  scenario "User adfds a new course" do
    visit new_course_path
    fill_in "Title", with: "Python course"
    fill_in "DEscription", with: "about python in 20 lesson"
    click_button 'Save'
    expect(page).to have_conent('Python course')
  end
end
