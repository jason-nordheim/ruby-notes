# Introduction and Background 

## What is Rails or 'Ruby on Rails'? 

1. A Framework 
2. A Gem (module)
3. A programming paradigm: "MVC" 
4. "Convention over configuration"
5. REST 

### Rails as a Web Framework
Rails fufill's mutliple development paradigms, but first and foremost 'Rails' or 'Ruby on Rails' is a web framework that provides developers with the tools to build web applications; short-cutting development time by having pre-built and customizable templates for things that are commonly needed in most web applications. Things such as; 
* routing 
* asset management 
* database connections 
* and much more 

#### Rails and MVC 
Rails was created with the concept of convention over configuration and this holds true for how the MVC structure was setup. **View** files correspond directly to **controller** files, which speak directly with **models**. As an example, imagine that you have a blog that has a database table called posts. You will have the following set of files:
* A `post.rb` model file that will contain: validations, database relationships, callbacks, and any custom logic for posts.
* A `posts_controller.rb` file that will have methods to manage data flow for the Post behavior, including the full set of CRUD features. The standard methods are: 
  * index
  * new
  * create
  * show
  * edit
  * update
  * destroy.
* A `views/` directory that will contain a corresponding view for each of the pages that the end user will access. For a CRUD based model, a few of the standard views would include: an index view to show all records, a show page that shows a specific record, and then new and edit pages that each render a form.

##### Controllers
The controllers connect the models, views, and routes or in other words; it manages data flow between the router, model, and views. 
* The view looks to the controller and only has access to the instance variables that the controller makes available. Those instance variables will contain any/all data coming in from the database.
* The routes file looks to the controller and ensures that the methods in the controller match the items in the routes file.

###### Controller Variable Scope 
`@model_name` variables defined in the controller are scoped so that the view's have access to them 

##### Models 
##### Views 
In a Rails application, the view files should contain the least amount of logic of any of the files in the model-view-controller architecture. The role of the view is to simply render whatever it is sent from the database.

Rails also does a great job of supplying built in `ActionView` helper methods that you can implement to efficiently code the views. For example, if you wanted to create a `div` for a set of blog posts that you want to iterate over, you can implement the following code:

```erb 
<%= content_tag(:div, @post, class: "post-index-page") do %>
  <%= content_tag(:p, "#{@post.title}: #{@post.summary}") %>
<% end %>
```
Which is translated to the following HTML markup:
```html 
<div id="post_42" class="post post-index-page">
  <p>My Amazing Blog Post: With an incredible summary</p>
</div>
```



### A Ruby Gem 
As a framework, Rails is a library of prebuilt code; and since it is Ruby, this is build into a Ruby gem. 


### MVC & Rails 
MVC or Model-View-Controller, is a design pattern in which we seperate application responsibilities of the application into models, controllers, and views:

1. models - represent the application data 
2. views - represent the application interface with the user 
3. controllers - represent (and are responsibile for) the core application logic

### Convention over configuration 
Rails follows a very specific convention... 

If you follow the conventions, you will get a lot of functionality for "free". You can override it by specifying overriding configuration; but this is not recomended. 

### Rails and REST

Think of 'REST' as a parallel for CRUD (Create, Read, Update, Delete)

| CRUD - Command | HTTP Equivilant | 
|:---|:---|
| Create | `POST` | 
| Read | `GET` | 
| Update | `PUT` / `PATCH` | 
| Delete | `DEL` | 


## What Rails is **NOT**

Rails is not: 
1. a programming langauge... as previously stated, Rails is a library of code written in Ruby. Ruby is the programming langauge; 'Rails' is the framework. 
2. slow... rails is designed to be performant, and optimizes (often seamlessly) web applications, but also hides the implementation of these performance optimizations and as a result can often result in bad practices for beginners that hop right into Rail's development. 



# Getting started 

## Make sure the `rails` gem is installed
To install it on your system, run the following command in the terminal of your computer:
```bash
gem install rails
```
> Depending on your system configuration, you may need to prepend the command with `sudo` to install the gem as the root user. Once the gem is installed you can create Rails applications!

## Create a new Rails application (from template)
To generate a new rails template, run the following command in Terminal: 
```bash
rails new blog-flash
``` 

This should generate a series of files that have a similar structure to this: 
```bash
├── app
│   ├── assets
│   │   ├── config
│   │   ├── images
│   │   └── stylesheets
│   ├── channels
│   │   └── application_cable
│   ├── controllers
│   │   └── concerns
│   ├── helpers
│   ├── javascript
│   │   ├── channels
│   │   └── packs
│   ├── jobs
│   ├── mailers
│   ├── models
│   │   └── concerns
│   └── views
│       └── layouts
├── bin
├── config
│   ├── environments
│   ├── initializers
│   └── locales
├── db
├── lib
│   ├── assets
│   └── tasks
├── log
├── public
├── storage
├── test
│   ├── channels
│   │   └── application_cable
│   ├── controllers
│   ├── fixtures
│   │   └── files
│   ├── helpers
│   ├── integration
│   ├── mailers
│   ├── models
│   └── system
├── tmp
│   ├── cache
│   │   ├── assets
│   │   └── bootsnap-compile-cache
│   │       ├── 00
│   │       ... 
│   │       ├── fe
│   │       └── ff
│   ├── pids
│   └── storage
└── vendorIs
```

### Folder structure and architecture 

| folder | description | 
|:---|:---| 
| `./app` | contains the models, views, controllers and the rest of the core functionality associated with the application. This is the one directory in which you can make a change and not have to restart the entire Rails serrver. |
| `./bin` | built-in Rails tasks, most of which will not require modification | 
| `./config` | manages a number of stettings that control the default behavior: This includes: environment settings, modules to be initializzed when the application starts, the ability to set langauge settings, application settings, database settings, routes, and a secret key base. | 
| `./db` | Contains the database schema file, `seeds.rb` file for seeding data. | 
| `./lib/tasks` | location of custom rake tasks. | 
| `./log` | contains the application logs, can be useful for debugging purposes, but for a production application it is often better to use an outside service as they can offer more features like querying and alerts. | 
| `./public` | directory containing custom error pages like 404 errors, along with the `robots.txt` file which will let develeopers control how search engines index the application on the web. | 
| `./test` | by default Rails will install the test suite in this directory. This is where all of your specs, factories, test helpers, and test configuration files can be found. Side note: We always use `RSpec`, which means this directory will actually be called spec. | 
| `./tmp` | this is where the temporary items are stored and is rarely accessed by developers. | 
| `./vendor` | this directory has been utilized for varying purposes in the past. In Rails 4+, its main purpose is for integrating Client-side MVC frameworks, such as AngularJS. | 






## Setup 

1. Build template `rails new app_name`
2. Setup Data Models (in the models folder)
  1. Create the Ruby class to model the data 
  2. Create a `rails` migration with the attributes you want the model to have using `rails g migration name_of_migration` 
3. (OPTIONAL) Seed test data 
  1. Seed the data with `rails db:seed` 
4. Setup Controller to provide access to those data model 
  1. Contollers (by convention) are declared in plural. 
  2. Controllers (by convention) are declared with an `index` method that returns all instances of the class that we match 
5. Setup Routes to the controller (`config>routes.rb`)



### Controller Setup 

```rb
class DogsController < ApplicationController 
  # by convention 
  def index
    @dogs = Dog.all 
    render json: @dogs 
end 
```



# Routing 

## Defining the root page 

In `routes.rb`, use the keyword `root` to define the index page for the site: 
```rb
Rails.application.routes.draw do 
  root = 'home#index' # ==> go to the home controller and execute the 'index" action 

```

## Setup Route

```rb
Rails.application.routes.draw do 
  get "/dogs", to: "dogs#index" # this is saying, go to the `dogs` controller, and call the `index` method

  # alternatively, if you want all the REST actions you can do 
  resources:dogs
end 
```

# Rails console 
The Rails console (accessed via: `rails c`) is an important tool in the arsenal of any Rails developer. It gives you a direct connection to your application's ecosystem and lets you perform tasks such as:
* Running database queries
* Running application code
* Performing full CRUD tasks with the database
* Allowing you to switch between making permanent database changes and running in a sandbox mode to test scripts out
* To start up the Rails 

## Some fun examples: (In the rails console) 
Suppose you have a blog website with posts. What if you want to find all of the posts from today? 
```rb
# find all the posts created between yesterday and tomorrow 
Post.where(created_at: Date.yesterday..Date.tomorrow).to_sql
# => "SELECT \"posts\".* FROM \"posts\" WHERE \"posts\".\"created_at\" BETWEEN '2020-04-21' AND '2020-04-23'"

# we can execute this query by removing the `to_sql` from the end 

```


# Beyond the Basics 



# Rails Generate 
You can generate code in `rails` by calling the `rails` alias in terminal, and then entering the arguments for what you would like to do 
```bash
# long hand 
rails generate controller people
# short-hand 
rails g generate controller people 
```

If you mess up anything, repeat the command, but substitute delete (`d`) instead of `g`. 
```bash 
rails d controller people 
```

If you want to generate a model and a controller (for an API), you can use the command: 
```bash 
# long-hand
rails generate resource Horse 
# short-hand 
rails g resource Horse 
```
## An example 
## An example 
What if I have a blog site and I want to quickly setup that functionality? Well that's something faily commmon, rails can build out the framework for you via a command called `scaffold`. You would use the `scaffold` command like so: 
```bash 
rails generate scaffold post title:string body:text
```
This will build out functionality for **all** of our CRUD operators for that data model. Let me stop and let's talk a little bit more about that. 

With that one command: `rails generate scaffold post title:string body:text`, I've told Rails: 
* I have this thing called a `post` that will store something called a `title`, and something else called a `body` 
* that `title` will have a string datatye - (i.e. it sh)
* that `body` will have a text datatype 

And with that information Rails has done the following: 
* It has generated 19 different files and modiefied 1 existing one 
  1. `db/migrate/20200422194620_create_posts.rb` - Rails created a database migration with the properties of the new object we've told Rails we want to create
  2. `app/models/post.rb` - Rails created a Model to represent that post
  3. `test/models/post_test.rb` - Rails created a test from a template to define tests to run related to your new object 
  4. `test/fixtures/posts.yml` - Rails created a outline of test data to run through your test 
  5. `app/controllers/posts_controller.rb` it created a controller to handle all of the crud operations for you including: `create`, `update`, `new`, `show`, and `destroy` along with working logic to handle that input. (This is huge!)
  6. It generated views for each of the CRUD operations: 
    1. `app/views/posts` - general posts 
    2. `app/views/posts/index.html.erb` - an index page 
    3. `app/views/posts/edit.html.erb` - an edit page (allows updating of object information)
    4. `app/views/posts/show.html.erb` - a page to display object data 
    5. `app/views/posts/new.html.erb` - a page where an end-user can enter information 
    6. `app/views/posts/_form.html.erb` - a partial page outlining shared code between the pages, mostly used in the event an error needs to be displayed on that page. 
  7. `test/controllers/posts_controller_test.rb` - a test file outlining tests for the associated controller 
  8. `test/system/posts_test.rb` - more tests 
  9. `app/helpers/posts_helper.rb` - a helper file for running tests 
  10. `app/views/posts/index.json.jbuilder` - a json option for retrieving objects by index 
  11. `app/views/posts/show.json.jbuilder` - a json return option for retrieving objects one or multiple object attributes 
  12. `app/views/posts/_post.json.jbuilder` - defines where to go redirect when returning json data 
  13. `app/assets/stylesheets/posts.scss` - a scss stylesheet  for the post object 
  14. `app/assets/stylesheets/scaffolds.scss` - a general scss stylesheet for stuff built as part of the `generate scaffold` 


That's 351 lines of code, written for you, for free. It creates all 20 of those files for you, and populates them with **working** code that will enable **ALL** of the CRUD operations. 

But wait... we can do more! 

Let's say we want to make our blog more interactive so we want to add the ability for people to comment on a post... for this we will likely need to store the data in our applications database. We could create a `comment.rb` model, a `comments_controller.rb`, a corresponding view folder, a default view and build all the routes manually, 
```bash
rails generate resource comment post:references body:text
```
With the command above, do all the stuff I did with `scaffold`, but Rails doesn't generate any views. 

But let's break down what's happening anyway... in one line, I've instructed Rails to build the model `comment.rb` with the attribute `body` with the data-type `text` and that a post `belongs_to` a post object... and Rails has generated the model, along with the standard CRUD operator functionality in the `routes.rb` and `comment_controller.rb` (including methods/actions for `create`, `show`, `update`, `index`, and `destroy`). 

What's crazy is we have the core functionality of a blog now.



# Creating a Migration 

You can create a migration by calling the `rails` alias in terminal, and then entering the arguments for what you would like to do 
```bash
rails g migration create_table_x name:string, age: integer  
```
| syntax | definition | 
|:--- |:---| 
| `rails` | rails alias |
| `g` | generate | 
| `migration` | indicates we are generating a db migration file | 
| `create_table_x` | the name of the file | 
| `name:string` | attribute:type | 
| `age:integer` | attribute: type | 


# General Rails Commands:

`rails -T` - lists all the rails commands 
`rails c` / `rails console` - launches interactive console to test the rails database 
`rails s` / `rails server` - launches your rails server. 
`rails routes` - displays the routes that the current rails app can handle 


# Rails URL Helpers 
Rails is meant to be flexible. As a result, there are typically a number of ways to accomplish the same goals. Routes are a great example of how this principle operates in a Rails app. You can route via a hard-coded path, or a route-helper (more flexible). 

In code that looks like this: 
```rb
# hard-coded path 
"/posts/#{@post.id}" 
# route helper 
post_path(@post)
```
What this is essentially saying is; "find the best way to a controller with this thing called a `post` based on looking at the instance `@post`. 

## Why use URL Helpers 

1. Route helpers are more dynamic - they are methods, not simply strings; since they are methods, that means if something changes with the route, often the code will not need to be changed as the method will still work. 

2. Route helpers clean up code - the code for a route-helper is much more readable. 
  * note: _you cannot use the helper methods within your model files_ 

3. Route helpers provide a more flexible mechanism for passing arguments - Without route-helpers, we would have to declare routes with string interpolation:
  * without route-helpers: `posts/<%= post.id %>?opt_in=true"` 
  * with route-helpers: `post_path(post, opt_in: true)` 

4. Route helpers directly translate into HTML-friendly paths - Using route-helpers eliminates unexpected characters in the URL, making redirection and redering more reliable. 

## Implementing Route Helpers 

### Configure the route 
In order to get routes for the posts, we need to handle `GET` on `/posts(.:format)` and direct that to the `posts#index` action as well as `GET` for `/posts/:id(.:format)` to the `posts#show` method. 

In the `routes.rb` that would look 
```rb
# config/routes.rb
resources :posts, only: [:index, :show]
```

| Prefix | HTTP Verb | Route Path | Controller Action | 
|:-------|:----------|:-----------|:------------------| 
| posts | `GET` | `/posts(.:format)` | `posts#index` | 
| post  | `GET` | `/posts/:id(.:format)` | `posts#show` | 

So the code in our view _could_ go from: 
```erb
<!-- without route helpers -->
<% @posts.each do |post| %>
  <div><a href='<%= "/posts/#{post.id}" %>'><%= post.title %></a></div>
<% end %>
``` 
to 
```erb 
<!-- with route-helpers -->
<% @posts.each do |post| %>
  <div><%= link_to post.title, "/posts/#{post.id}" %></div>
<% end %>
``` 

[Link to lab](https://github.com/jason-nordheim/rails-url-helpers-readme-denver-web-033020)

# Active Record 
## Parent Child Relationships 
You can create a parent child relationship using ActiveRecord using the methods: `has_many` and `belongs_to`. In order for this to be bi-directional, both classes must use these methods. 

An example: 

```rb 
# /app/models/post.rb 
class Posts < ActiveRecord 
  has_many :comments #plural 
end 

# /app/models/comment.rb 
class Comment < ActiveRecord
  belongs_to :post  # singular 
end 

# and in the migration would look like" 
class CreateComments < ActiveRecord::Migration[6.0]
  def change
    create_table :comments do |t|
      t.references :post, null: false, foreign_key: true
      t.text :body

      t.timestamps
    end
  end
end
``` 

# Partials 

`.html.erb` files that are sub templates of a full-view --> they represent part of what is being displayed, and as such are never displayed on their own, but rather alongside a dedicated view. 
* Enables re-use of repetitive displayed components 
* Allows for greater seperation of concerns