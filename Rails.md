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

