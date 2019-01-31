# App setup
By the end of this section, you'll have a Rails app setup as an API with one test route.  You'll be able to receive JSON requests, and respond with data encoded in JSON format.

## Let's get started
We're going to use the ```--api``` flag when building a new Rails application to customize our new Rails app to have just what we need.  The app communicates in JSON, instead of HTML/CSS/Javascript, so we don't need to clutter the app up with support for all of those file types.  Open up a command line prompt, and enter the following commands:

```
$ gem install rails
$ rails new cat_tinder_backend --api -T --database=postgresql
$ cd cat_tinder_backend
```
This gets the latest and greatest version of Rails, and generates a new Rails application configured to be used as an API.  the ```-T``` flag tells rails to skip adding the default Minitest framework, as we're going to use Rspec instead.

````
$ echo "gem 'rspec-rails', groups: [:development, :test]" >> Gemfile
$ bundle install
$ rails generate rspec:install
```
This adds 'rspec-rails' to the Gemfile, and instructs Rails to only load rspec when we are in development or test mode, and not production.  The ```rails g rspec:install``` command installs all the necessary files to create and run our tests.

Next its time to add a Cat resource.  The following command will add the Model, Migration, Controller, and Route for cats.
```
$ rails g resource cat name:string age:integer enjoys:text
$ rake db:create db:migrate
````

## Verify that we're all set up
Let's take a look around the application and verify that everything is setup correctly.  The first thing we can do is see that our test suite is running.  Of course, we don't have any specs yet, so we won't get much feedback, but rspec itself should run and finish successfully:

```
$ rspec spec
*

Pending: (Failures listed here are expected and do not affect your suite's status)

  1) Cat add some examples to (or delete) .../cat_tinder_backend/spec/models/cat_spec.rb
     # Not yet implemented
     # ./spec/models/cat_spec.rb:4


Finished in 0.01159 seconds (files took 2.77 seconds to load)
1 example, 0 failures, 1 pending
```

Looks good!  If we open up Atom and inspect our app, we should see the following file structure:
![cat tinder files](https://s3.amazonaws.com/learn-site/curriculum/cat-tinder/cat_tinder_server_files.png)

Open up ```db/migrate/``` (yours will be named slightly different)

```Ruby
class CreateCats < ActiveRecord::Migration[5.1]
  def change
    create_table :cats do |t|
      t.string :name
      t.integer :age
      t.text :enjoys

      t.timestamps
    end
  end
end
```

If we look in ``` config/routes.rb ```, we should see our cats route there:

```ruby
Rails.application.routes.draw do
  resources :cats
  # For details on the DSL available within this file, see http://guides.rubyonrails.org/routing.html
end
```

With one last check, we can be pretty confident that everything is setup correctly.  Let's fire up a Rails console, and interact with the database:

```
$ rails c
Running via Spring preloader in process 22833
Loading development environment (Rails 5.1.5)
2.4.1 :001 > Cat.create(name: 'Felix', age: 4, enjoys: 'Window ledges, being in charge, and cat food, lots and lots of cat food.')
   (0.1ms)  begin transaction
  SQL (1.3ms)  INSERT INTO "cats" ("name", "age", "enjoys", "created_at", "updated_at") VALUES (?, ?, ?, ?, ?)  [["name", "Felix"], ["age", 4], ["enjoys", "Window ledges, being in charge, and cat food, lots and lots of cat food."], ["created_at", "2018-03-09 16:01:41.355922"], ["updated_at", "2018-03-09 16:01:41.355922"]]
   (1.1ms)  commit transaction
 => #<Cat id: 1, name: "Felix", age: 4, enjoys: "Window ledges, being in charge, and cat food, lots...", created_at: "2018-03-09 16:01:41", updated_at: "2018-03-09 16:01:41">
2.4.1 :002 > Cat.all
  Cat Load (0.3ms)  SELECT  "cats".* FROM "cats" LIMIT ?  [["LIMIT", 11]]
 => #<ActiveRecord::Relation [#<Cat id: 1, name: "Felix", age: 4, enjoys: "Window ledges, being in charge, and cat food, lots...", created_at: "2018-03-09 16:01:41", updated_at: "2018-03-09 16:01:41">]>
2.4.1 :003 >
```

That looks great!  In the next step, we'll expose some endpoints in our API, so the frontend application has a way to communicate with all the functionality we've built out so far.