![General Assembly Logo](http://i.imgur.com/ke8USTq.png)

# Rails API: One-To-Many

So far you've seen how to associate records with one another using foreign keys
 in a database.
Just as we can use ActiveRecord to read, change, update, and delete data from
 our database, we can use ActiveRecord relationship methods to associate records
 with one another using Ruby code.

## Prerequisites

This lesson assumes you have forked and cloned the following:

-   [rails-api-library-demo](https://github.com/ga-wdi-boston/rails-api-library-demo)
-   [rails-api-clinic-code-along](https://github.com/ga-wdi-boston/rails-api-clinic-code-along)
-   [rails-api-cookbook-lab](https://github.com/ga-wdi-boston/rails-api-cookbook-lab)

We will be working from the `training/one-to-many` branches of each.

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

We've got a single resource and all of its components (routes, controller,
model, migration) for each domain we're working in. Let's go in and create a
second resource for each.

### Demo: Create Author Routes and Controller

In [rails-api-library-demo](https://github.com/ga-wdi-boston/rails-api-library-demo),
you've seen a `books` resource created.

In order to create a pairing `author` resouce, we'll need to start with our
first lines of action: a route, then controller. Pay attention as I create
these.

> Note: using Rails' `resources :<resource_name>` creates all 7 default resource
> routes (`index`, `show`, `create`, `update`, `delete`, `new`, `edit`).
> `new` and `edit` controller actions are only used with views, so typically
> with API routes, it is safe to declare
> `resources :<resource_name>, except: [:new, :edit]`

### Code Along: Create Doctor Routes and Controller

We're going to go through the same motions as my demo and create resource
routes and a controller for a `doctors` resource.

### Lab: Create Recipe Routes and Controller

Work methodically in [rails-api-cookbook-lab](https://github.com/ga-wdi-boston/rails-api-cookbook-lab)
to first create resource routes for `recipes`.

Once your resource routes are created, create a `RecipesController` with the 5
default API controller actions.

### Demo: Create Author Model

We've created our routes and controller for the `authors` resource, but we're
now stuck at the following error:

> `uninitialized constant AuthorsController::Author`

The `::Author` portion of this should indicate to you that an `Author` model is

> As a reminder, generator short-hand for model creation is:
> `rails generate model author given_name surname`

### Code Along: Create Doctor Model

Let's create a `Doctor` model with `given_name` and `surname` fields and run
migrations.

### Lab: Create Recipe Model

Go ahead and create a `Recipe` model with `name` and `family_favorite`
(boolean) fields.  Don't forget to run your migration!

Once that's created, use your `rails console` to create a recipe. See if you
can access them at localhost:3000/recipes.

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
