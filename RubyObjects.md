# Object Attributes

## Getters and Setters 
In Ruby, getters and setters are commonly referred to as "readers" (`attr_reader`) and "writers" (`attr_writer`), and are most often composed with the use of symbols. So instead of writing functions, we can use `attr_reader` and `attr_writer` to create "getters" and "setters" for our class attributes. Additional, if we want to specify an attribute that can be both read & written, we can use an `attr_accessor` which creates both read and write functionality for a class attribute. 

Code Demonstration 
```rb 
# Explicitely Defining Read/Write 
class Employee 
  def initialize name, address, start_date 
    @name = name 
    @address = address 
    @start_date = start_date 
  end 
  # getter 
  def name 
    @name 
  end
  # getter 
  def address
    @address 
  end 
  def start_date 
    @start_date 
  end 
  # setter 
  def name=(name)
    @name = name 
  end 
  # setter 
  def address=(address)
    @address = address 
  end 
end 

# The Same class defined using reader 
class Employee 
  attr_reader :start_date 
  attr_accessor :name, :address 
  def initialize name, address, start_date
    @name = name 
    @address = address
    @start_date = start_date 
  end 
end 

```


# Inheritance & Polymorphism 

There are two ways to re-use code in Ruby: 
1. Inheritance 
2. Modules 

## Inheritance 

Ruby supports **Single Inheritance**, in other words; every class in Ruby has 1 and exactly 1 super class. This is specified using the `<` symbol after the class declaration like so: 

```rb
class User 
  attr_reader :name 
  def initialize(name)
    @name = name
  end 
end 

class AdminUser < User 
  def is_admin?
    true
  end 
end 
```
A class will inherit all attributes and methods of the super class _unless_ it explicity overrides or removes them. Every object in Ruby stems (or inherits from) `BasicObject` (including the `Object` class). 

Since Ruby classes are **NEVER** finalized, we can re-open any of these classes and modify them however we want... so if I wanted to add a method to **all** classes in Ruby, I could re-open the `Object` class and add a new method. Every class that inherits from that class would still inherit from `Object` and as a result, would now have the functionality provided by my modification to the class: 

```rb 
➜ irb
➜ class EmptyClass; end
#=> nil
➜ obj = EmptyClass.new
#=> #<EmptyClass:0x00007ff023902868>
➜  obj.ping
# NoMethodError (undefined method `ping' for #<EmptyClass:0x00007ff023902868>)
➜ class Object
➜   def ping
➜     "pong"
➜    end
➜  end
#=> :ping
➜  obj.ping
#=> "pong"
➜  7.ping
#=> "pong"
```

### Understanding where a method came from (finding the root object)

As previously satted, classes all inherit from the `BasicObject` class, and unless we specify otherwise, **all** classes will inherit the methods and attributes of their parent classes. Sometimes it may be pertinent to investigate where a method or attribute is derived from... 

... to do this with the method class:
```rb 
➜ irb
➜ class EmptyClass; end
#=> nil
➜ obj = EmptyClass.new
#=> #<EmptyClass:0x00007ff023902868>
➜ class Object
➜   def ping
➜     "pong"
➜    end
➜  end
#=> :ping
➜ m = obj.method(:ping)
#=> #<Method: EmptyClass(Object)#ping>
➜ m.reciever 
#=> #<EmptyClass:0x00007ff023902868>
➜ m.owner
#=> Object
```

## Modules 

### What is a module, and what is it used for? 
What is a module? Well, in Ruby a module is technically a super-class of class, but in more verbose terms; a Ruby module is really just a collection of methods. One difference between modules and classes in Ruby is that while a Ruby class can only inherit one super-class, it can inherit as many modules as you needed to gain the desired functionality. 

### How do we use modules? 
By declaring a `module`, we can define a set of attributes and methods that we may want to use in other classes. We can then add these atributes and methods to any class by calling `include` within the class we want to add those methods and/or attributes to. 

An example: 
```rb 
# Pull in date module 
require 'date' 
# 
# declare 'employee' module 
# 
module Employee 
  attr_accessor :start_date 

  def employment_length 
    day = Date.today - start_date.to_date 
  end 
end 
# => :employment_length 

#
# Now we can add the module to the class 'User' 
# 
class User 
  include Employee  # this makes all of the methods inside the module available inside the class 
end 
# => User 
```

Another way we can use modules is via the `extend` keyword/function. While all previously stated rules about inheritance hold true (a class can only inherit a single super-class, but can `include` as many modules as desired), if we want to add functionality to a single instance of a class, without changing the functionalituy of all instances of a class, we can use the `extend` keyword. 

With the example below, the instance of `User` (`user`) has all the functionality of an `Employee` class, but the `User` class does not - in other words; only the instance that `extend`ed `Employee` recieved that modules attributes and methods. 
```rb 
# Pull in date module 
require 'date' 
# 
# declare 'employee' module 
# 
module Employee 
  attr_accessor :start_date 

  def employment_length 
    day = Date.today - start_date.to_date 
  end 
end 
# => :employment_length 

#
# Now we can add the module to the class 'User' 
# 
class User 
end 
# => User 
user = User.new 
# => #<User:0x007fba6c123698>
user.extend(Employee) 
# => #<User:0x007fba6c123698>
```
Using `extend` effectivily creates a singleton instance of that class, and applies the methods to that single-ton instance. We can illustrate this in IRB like so:
```rb
User.public_instance_methods.grep(/start_date/)
# => [] 
another_user = User.new 
# => #<User:0x007fba6d4ec8a0>
another_user.methods.grep(/start_date/)
# => [] 
user.methods.grep(/start_date/)
# => [:start_date, :start_date=]
user.singleton_class.public_instance_methods.grep(/start_date/)
# => [:start_date, :start_date=]
``` 

## Method Dispatch 

"Method Dispatch" is just a fancy way of saying, when a method (of an object) is called, how does Ruby determine where that method was defined? In other words, was it within the class that the method was called on? Was it part of that class's super-class? Or the class's super-class's super-class? 

Ruby determines this in the following manner: Ruby looks at the instance of the class, and sees if the method/attribute is defined in the single-ton instance of that class. If it is defined there, than that method/attribute is called upon. If the single-ton instance of the does **not** define the method or attribute, Ruby checks the class definition upon which the single-ton instance was created, which for consistency could also be called the "super-class" of the single-ton instance. From here Ruby proceeds up the super-class inheritance hierarchy until it finds the definition of the requested method or attribute. If  it reaches `BasicObject` and still has not found the requested method or attribute, Ruby goes back to the single-ton instance of the class, and looks for a `method_missing` method. This is a special method that defines what to do when a method is missing and cannot be found. This repeats the checks all the way through the inheritance heirarchy (i.e. check's the single-ton instance of the class for a `missing_method` method, then the class of for a `method_missing`, then the super-class of that class, and so on until it goes all the way back to `BasicObject`). If `method_missing` cannot be found all the way in the inheritance hierarchy, Ruby raises a `NoMethodError`. 

### Defining `method_missing` 

If you want to define your own `method_missing` function, you would use the following format: `Class.method_missing(name, *args, &block)` where the `Class` is the name of the class, `name` is the name of the method we are searching for, `*args` as a `splat` or an array of the arguments, that are being passed to the method, and lastly; the `&block` defines the optional block parameter. 

```rb
# Format 
Class.method_missing(name, *args, &block) 

# Example
class AnyP
  #defining a missing method function for any method that starts with the letter 'P' 
  def method_missing(name, *args)
    # name is a symbol, so first we need to convert it to a string 
    if name.to_s.starts_with?('p')
      "You called #{name} with #{args.inspect}" 
    else 
      super #if name does not start with 'p' check the super class for a missing_method on what to do
    end 
  end 
end 
```