![General Assembly Logo](http://i.imgur.com/ke8USTq.png)

# Rails API: One-To-Many

So far you've seen how to associate records with one another using foreign keys
 in a database.
Just as we can use ActiveRecord to read, change, update, and delete data from
 our database, we can use ActiveRecord relationship methods to associate records
 with one another using Ruby code.

## Objectives

-   Digram the database tables and Entity Relationship Diagram that describe a
 one-to-many relationship.
-   Write a migration for a one-to-many relationship.
-   Associate plain Ruby objects with one another.
-   Compare `has_many` and `belongs_to` to other macros, like `attr_accessor`.
-   Configure ActiveRecord to manage one-to-many relationships using `has_many`
 and `belongs_to`.
-   Create associated records using the rails console.

## Preparation

1.  Fork and clone this repository.
1.  Change into the new directory.
1.  Install dependencies with `bundle install`.
1.  Add secrets to `config/secrets.yml`.
1.  Create a database with `bundle exec rake db:create`.
1.  Create a database schema with `bundle exec rake db:migrate`.
1.  Run the HTTP server with `bundle exec rails server`.

## Multiple Resources

### Demo: Create Author Routes and Controller

### Code Along: Create Doctor Routes and Controller

### Lab: Create Recipe Routes and Controller

## `has_many`

### Demo: Author `has_many` Books

### Code Along: Doctor `has_many` Patients

### Lab: Recipe `has_many` Ingredients

## `belongs_to`

### Demo: Book `belongs_to` Author

### Code Along: Patient `belongs_to` Doctor

### Lab: Ingredient `belongs_to` Recipe

## Modifying Migrations

## Further Reading

-   [Rails Association Basics](http://guides.rubyonrails.org/association_basics.html)
 Read the sections on belongs_to and has_many.
-   [ActiveRecord Basics](http://guides.rubyonrails.org/active_record_basics.html)
-   [Rails Documentation](http://api.rubyonrails.org/)
-   [Debugging Rails with the byebug Gem](http://guides.rubyonrails.org/debugging_rails_applications.html#debugging-with-the-byebug-gem)
-   [With So Much Rails to Learn, Where Do You Start?](http://www.justinweiss.com/blog/2015/05/25/with-so-much-rails-to-learn/)

## [License](LICENSE)

Source code distributed under the MIT license. Text and other assets copyright
General Assembly, Inc., all rights reserved.
