![General Assembly Logo](http://i.imgur.com/ke8USTq.png)

# Rails API: One-To-Many

So far you've seen how to associate records with one another using foreign keys
 in a database.
Just as we can use ActiveRecord to read, change, update, and delete data from
 our database, we can use ActiveRecord relationship methods to associate records
 with one another using Ruby code.

## Prerequisites

This lesson assumes you have gone through -   [Rails API: Single
 Resource](https://github.com/ga-wdi-boston/rails-api-single-resource) with the
 following:

-   [Library API](https://github.com/ga-wdi-boston/rails-api-library-demo)
-   [Clinic API](https://github.com/ga-wdi-boston/rails-api-clinic-code-along)
-   [Cookbook API](https://github.com/ga-wdi-boston/rails-api-cookbook-lab)

If you are behind, or don't have correct code, please speak with the instructor
immediately so you don't fall further behind.

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

## Multiple Resources

We've got a single resource and all of its components (routes, controller,
model, migration) for each domain we're working in. Let's go in and create a
second resource for each.

### Demo: Scaffold Author Routes, Controller, Model, and Serializer

In [rails-api-library-demo](https://github.com/ga-wdi-boston/rails-api-library-demo),
you've seen a `books` resource created.

In order to create a pairing `author` resouce, we'll need to repeat what was done in the last talk. However, since we've seen this already, we're going to use a generator that creates more than one piece at a time, and modify it accordingly.

### Demo: Create Author Model

If we open a browser and hit `/authors` we get back: `No route matches [GET] \"/authors\"`, which makes sense. We haven't done *anything* with authors yet.

In order to generate the code we wrote by hand for `patients` we can use the following (shortcut) command:
> `bin/rails generate scaffold author given_name:string family_name:string specialty:string gender:string`

Now let's examine each of the files it created!
```
~/wdi/training/rails-api-library-demo (tutorial)$ bin/rails generate scaffold author given_name:string family_name:string specialty:string gender:string
Running via Spring preloader in process 17246
Expected string default value for '--serializer'; got true (boolean)
      invoke  active_record
      create    db/migrate/20170419183303_create_authors.rb
      create    app/models/author.rb
      invoke    rspec
      create      spec/models/author_spec.rb
      invoke  resource_route
       route    resources :authors
      invoke  serializer
      create    app/serializers/author_serializer.rb
      invoke  scaffold_controller
      create    app/controllers/authors_controller.rb
      invoke    rspec
      create      spec/controllers/authors_controller_spec.rb
      create      spec/routing/authors_routing_spec.rb
      invoke      rspec
      create        spec/requests/authors_spec.rb
```

## Migration File

`create    db/migrate/20170419183303_create_authors.rb`

This file sets up our migration using the command-line arguments we passed
with `bin/rails generate scaffold` command. Since we haven't migrated yet,
we can still modify this file to make some values required.
```diff
class CreateAuthors < ActiveRecord::Migration[5.0]
  def change
    create_table :authors do |t|
-      t.string :given_name
+      t.string :given_name, null: false
-      t.string :family_name
+      t.string :family_name, null: false
      t.string :specialty
      t.string :gender

      t.timestamps
    end
  end
end
```

### Code Along: Create Doctor Model

Let's create a `Doctor` model with `given_name` and `surname` fields and run
migrations.

### Lab: Create Recipe Model

Go ahead and create a `Recipe` model with `name` and `family_favorite`
(boolean) fields.  Don't forget to run your migration!

Once that's created, use your `rails console` to create a recipe. See if you
can access them at localhost:4147/recipes.

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

To complete this model relationship in Rails, the other side of the
relationship must use the `belongs_to` macro.

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
bin/rails generate migration AddAuthorToBooks author:references
```

Let's play with our results in `bin/rails console`.

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
