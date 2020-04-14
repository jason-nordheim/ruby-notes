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

A module in Ruby is really just a collection of methods. 