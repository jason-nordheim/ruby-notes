# Introduction and Background 

## What is Rails or 'Ruby on Rails'? 

1. A Framework 
2. A Gem (module)
3. A programming paradigm: "MVC" 

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
│   │       ├── 01
│   │       ├── 02
│   │       ├── 03
│   │       ├── 04
│   │       ├── 05
│   │       ├── 06
│   │       ├── 07
│   │       ├── 08
│   │       ├── 09
│   │       ├── 0a
│   │       ├── 0b
│   │       ├── 0c
│   │       ├── 0d
│   │       ├── 0e
│   │       ├── 0f
│   │       ├── 10
│   │       ├── 11
│   │       ├── 12
│   │       ├── 13
│   │       ├── 14
│   │       ├── 15
│   │       ├── 16
│   │       ├── 17
│   │       ├── 18
│   │       ├── 19
│   │       ├── 1a
│   │       ├── 1b
│   │       ├── 1c
│   │       ├── 1d
│   │       ├── 1e
│   │       ├── 1f
│   │       ├── 20
│   │       ├── 21
│   │       ├── 22
│   │       ├── 23
│   │       ├── 24
│   │       ├── 25
│   │       ├── 26
│   │       ├── 27
│   │       ├── 28
│   │       ├── 29
│   │       ├── 2a
│   │       ├── 2b
│   │       ├── 2c
│   │       ├── 2d
│   │       ├── 2e
│   │       ├── 2f
│   │       ├── 30
│   │       ├── 31
│   │       ├── 32
│   │       ├── 33
│   │       ├── 34
│   │       ├── 35
│   │       ├── 36
│   │       ├── 37
│   │       ├── 38
│   │       ├── 39
│   │       ├── 3a
│   │       ├── 3b
│   │       ├── 3c
│   │       ├── 3d
│   │       ├── 3e
│   │       ├── 3f
│   │       ├── 40
│   │       ├── 41
│   │       ├── 42
│   │       ├── 43
│   │       ├── 44
│   │       ├── 45
│   │       ├── 46
│   │       ├── 47
│   │       ├── 48
│   │       ├── 49
│   │       ├── 4a
│   │       ├── 4b
│   │       ├── 4c
│   │       ├── 4d
│   │       ├── 4e
│   │       ├── 4f
│   │       ├── 50
│   │       ├── 51
│   │       ├── 52
│   │       ├── 53
│   │       ├── 54
│   │       ├── 55
│   │       ├── 56
│   │       ├── 57
│   │       ├── 58
│   │       ├── 59
│   │       ├── 5a
│   │       ├── 5b
│   │       ├── 5c
│   │       ├── 5d
│   │       ├── 5e
│   │       ├── 5f
│   │       ├── 60
│   │       ├── 61
│   │       ├── 62
│   │       ├── 63
│   │       ├── 64
│   │       ├── 65
│   │       ├── 66
│   │       ├── 67
│   │       ├── 68
│   │       ├── 69
│   │       ├── 6a
│   │       ├── 6b
│   │       ├── 6c
│   │       ├── 6d
│   │       ├── 6e
│   │       ├── 6f
│   │       ├── 70
│   │       ├── 71
│   │       ├── 72
│   │       ├── 73
│   │       ├── 74
│   │       ├── 75
│   │       ├── 76
│   │       ├── 77
│   │       ├── 78
│   │       ├── 79
│   │       ├── 7a
│   │       ├── 7b
│   │       ├── 7c
│   │       ├── 7d
│   │       ├── 7e
│   │       ├── 7f
│   │       ├── 80
│   │       ├── 81
│   │       ├── 82
│   │       ├── 83
│   │       ├── 84
│   │       ├── 85
│   │       ├── 86
│   │       ├── 87
│   │       ├── 88
│   │       ├── 89
│   │       ├── 8a
│   │       ├── 8b
│   │       ├── 8c
│   │       ├── 8d
│   │       ├── 8e
│   │       ├── 8f
│   │       ├── 90
│   │       ├── 91
│   │       ├── 92
│   │       ├── 93
│   │       ├── 94
│   │       ├── 95
│   │       ├── 96
│   │       ├── 97
│   │       ├── 98
│   │       ├── 99
│   │       ├── 9a
│   │       ├── 9b
│   │       ├── 9c
│   │       ├── 9d
│   │       ├── 9e
│   │       ├── 9f
│   │       ├── a0
│   │       ├── a1
│   │       ├── a2
│   │       ├── a3
│   │       ├── a4
│   │       ├── a5
│   │       ├── a6
│   │       ├── a7
│   │       ├── a8
│   │       ├── a9
│   │       ├── aa
│   │       ├── ab
│   │       ├── ac
│   │       ├── ad
│   │       ├── ae
│   │       ├── af
│   │       ├── b0
│   │       ├── b1
│   │       ├── b2
│   │       ├── b3
│   │       ├── b4
│   │       ├── b5
│   │       ├── b6
│   │       ├── b7
│   │       ├── b8
│   │       ├── b9
│   │       ├── ba
│   │       ├── bb
│   │       ├── bc
│   │       ├── bd
│   │       ├── be
│   │       ├── bf
│   │       ├── c0
│   │       ├── c1
│   │       ├── c2
│   │       ├── c3
│   │       ├── c4
│   │       ├── c5
│   │       ├── c6
│   │       ├── c7
│   │       ├── c8
│   │       ├── c9
│   │       ├── ca
│   │       ├── cb
│   │       ├── cc
│   │       ├── cd
│   │       ├── ce
│   │       ├── cf
│   │       ├── d0
│   │       ├── d1
│   │       ├── d2
│   │       ├── d3
│   │       ├── d4
│   │       ├── d5
│   │       ├── d6
│   │       ├── d7
│   │       ├── d8
│   │       ├── d9
│   │       ├── da
│   │       ├── db
│   │       ├── dc
│   │       ├── dd
│   │       ├── de
│   │       ├── df
│   │       ├── e0
│   │       ├── e1
│   │       ├── e2
│   │       ├── e3
│   │       ├── e4
│   │       ├── e5
│   │       ├── e6
│   │       ├── e7
│   │       ├── e8
│   │       ├── e9
│   │       ├── ea
│   │       ├── eb
│   │       ├── ec
│   │       ├── ed
│   │       ├── ee
│   │       ├── ef
│   │       ├── f0
│   │       ├── f1
│   │       ├── f2
│   │       ├── f3
│   │       ├── f4
│   │       ├── f5
│   │       ├── f6
│   │       ├── f8
│   │       ├── f9
│   │       ├── fa
│   │       ├── fb
│   │       ├── fc
│   │       ├── fd
│   │       ├── fe
│   │       └── ff
│   ├── pids
│   └── storage
└── vendorIs
```