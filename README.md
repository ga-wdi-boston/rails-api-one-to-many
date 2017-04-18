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

-   Diagram the database tables and Entity Relationship Diagram that describe a
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
routes and a controller for a `doctors` resource in [rails-api-clinic-code-along](https://github.com/ga-wdi-boston/rails-api-clinic-code-along).

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
either erroneous or, as it is in this case, missing.

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

Often, the resources of our application will have relationships with each
other. In our three domains, authors have many books, doctors have many
patients, and recipes have many ingredients.

Versus having ownership information writen in two different tables (i.e.,
doctors' info saved to their own table as well as rewritten in the patients'
table), we want to make sure we set up a foreign key association between the
two.

How can we reflect this in Rails?

Simple. We begin by applying the `has_many` macro to the parent resource models.

### Demo: Author `has_many` Books

I'll apply the `has_many` macro to the Author model.

Once doing this, the `has_many` macro provides us with many useful getters and
setters:

```rb
Author#books
Author#books<<
Author#books.delete
Author#books.destroy
Author#books=
Author#book_ids
Author#book_ids=
Author#books.clear
Author#books.empty?
Author#books.size
Author#books.find
Author#books.exists?
Author#books.build
Author#books.create
Author#books.create!
```

## `belongs_to`

To complete this model relationship in Rails, the class on the `many` side must
use the `belongs_to` macro.

### Demo: Book `belongs_to` Author

Watch as I add this macro to the Book model. Take note of singular vs. plural
conventions for both `belongs_to` and `has_many`.

### Code Along: Doctor `has_many` Patients, Patient `belongs_to` Doctor

Let's add `has_many` and `belongs_to` macros where appropriate for our doctors
to have many patients and our patients to belong to a doctor.

### Lab: Recipe `has_many` Ingredients, Ingredient `belongs_to` Recipe

Go ahead and set up recipes to have many ingredients, and ingredients to belong
to a recipe.

## Modifying Migrations

We've almost finished with our relationships. We need one last thing - a
foreign key reference column on our books, patients, and ingredients tables.
This will allow us to reference the respective author, doctor, and recipe each
instance belongs to by ID.

## Demo: Modify Books Migration

To update our `books` migration, we have a couple of options:

1.  Hand-edit our existing books migration, rollback our database, and remigrate
1.  Generate a migration change to add a foreign key column to our books table

We'll be going with the latter. Why? Remember that migrations occur in the
order of their timestamps. If we go in and modify our books migration (which,
in theory, has an earlier timestamp than the authors migration), and make a
reference to the authors table before it exists, our migration will fail.

Watch as I generate this migration change with:

```ruby
rails g migration AddAuthorToBooks author:references
```

Let's play with our results in `rails console`.

## Code Along: Modify Patients Migration

Together, let's run a migration to add a `doctor` column with the appropriate
 reference to your `patients` table.

## Lab: Modify Ingredients Migration

Your turn! Run a migration to add a `recipe` column with the appropriate
 reference to your `ingredients` table.

## Further Reading

-   [Rails Association Basics](http://guides.rubyonrails.org/association_basics.html)
 Read the sections on belongs_to and has_many.
-   [ActiveRecord Basics](http://guides.rubyonrails.org/active_record_basics.html)
-   [Rails Documentation](http://api.rubyonrails.org/)
-   [Debugging Rails with the byebug Gem](http://guides.rubyonrails.org/debugging_rails_applications.html#debugging-with-the-byebug-gem)
-   [With So Much Rails to Learn, Where Do You Start?](http://www.justinweiss.com/blog/2015/05/25/with-so-much-rails-to-learn/)

## [License](LICENSE)

1.  All content is licensed under a CC­BY­NC­SA 4.0 license.
1.  All software code is licensed under GNU GPLv3. For commercial use or alternative
licensing, please contact legal@ga.co.
