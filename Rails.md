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

### Setup Route

```rb
Rails.application.routes.draw do 
  get "/dogs", to: "dogs#index" # this is saying, go to the `dogs` controller, and call the `index` method

  # alternatively, if you want all the REST actions you can do 
  resources:dogs
end 
```

## Rails console 
The Rails console (accessed via: `rails c`) is an important tool in the arsenal of any Rails developer. It gives you a direct connection to your application's ecosystem and lets you perform tasks such as:
* Running database queries
* Running application code
* Performing full CRUD tasks with the database
* Allowing you to switch between making permanent database changes and running in a sandbox mode to test scripts out
* To start up the Rails 


# Beyond the Basics 


# Rails Generate 
You can generate code in `rails` by calling the `rails` alias in terminal, and then entering the arguments for what you would like to do 
```bash
# long hand 
rails generate 
# short-hand 
rails g 
```

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


# Rails Commands:

`rails -T` - lists all the rails commands 
`rails c` / `rails console` - launches interactive console to test the rails database 
`rails s` / `rails server` - launches your rails server. 
`rails routes` - displays the routes that the current rails app can handle 