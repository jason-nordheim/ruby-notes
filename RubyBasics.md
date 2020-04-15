# Key Ideas in Ruby 
* Object Orientation
  * Duck Typing 
  * Method dispatch 
  * Classes & Constants
* Functional Programming 
  * Procs, blocks, lambdas 
  * Pure functional Ruby 
  * How functional programming can help us become better developers
* Metaprogramming 
  * Create new programming languages (almost)
  * Use Ruby to write more Ruby 

# Ruby and OOP 
## Ruby as an Object-Oriented Langauge 
### _Almost_ everything is an object 
Pretty much everything in Ruby is an object: 
* Methods
* User-defined Classes
* Modules 
* Arrays 

There are some exceptions: 
* Numbers: `Fixnum`, `Rational`, `Float`
* Text: `String` 
* Booleans: `True`, `False`
* Symbols: `Symbol`

#### What is an object? 
Key Tenants: 
* Objects have distinct local state 
* Objects can interact with other objects 
* Object cannot control other objects 

What is an object? 
* A collection of references to other objects 
* defined set of messages that responds 
* Has internal state 
## Defining methods & classes 
### Classes 
* Classes must start with a capital letter, and are (by convention) written in camel case.
* Classes are constructed or initialized with the `initialize` method, which is called by default when the class is instantiated. 
* Instance variables begin with a single `@` sign
* Ruby is a dynamic langauge. Part of that means that no class definition is **ever** finalized; which means that we can re-open and add, remove or modify class behavior at **any** time simply be redefining the class. 
* You instantiate an instance of a class by calling `ClassName.new` then passing any arguments required for construction. 
### Methods 
* Methods (within classes) start witha _lowercase_ letter 
* Methods are declared in all lower case, and seperated by underscores (`_`)
* Methods **can** end with a symbol
  * Methods that return `true` or `false` (by convention) end with a `?`  (see `even?` for an example)
  * Methods that perform unexpected behavior, could raise an exception or result in destructive behavior (by convention) end with a `!` (see `select!` for example)
* Class methods ("static methods" in other languages) are prefixed
  * Class methods are evaluated within the context of the class, so calling `new` within a class method will construct a new instance of that class. 
* Accessor methods are simply titled after the attribute they are return 
* Mutator methods are (by convention) titled with the name followed by an `=` and acccept the variable of the attribute they are setting 
* Parameters of methods can be given default values using `=default_value`, allowing us to omit that argument when calling the method
* Optional parameters must be either first, or last in the parameter list (you cannot declare a optional first and last parameter with required parameters in between)
  * best-practice is to only have one optional parameter per method and to declare that parameter last. 
### Demonstration of class & methods definitions 
```rb 
require 'date' 
class User 
  # getter (using attr_reader)
  attr_reader :name 
  # setter (using attr_reader) 
  attr_writer :name 
  # attr
  # Constructor 
  def initialize(name, date_of_birth)
    @name = name 
    days_since_birth = Date.today - Date.parse(date_of_birth)
    @age = days_since_birth / 365 
  end 
  # Accessor Method 
  def name 
    @name 
  end 
  # Mutator Method 
  def name=(name)
    @name = name 
  end 
  # boolean instance method 
  def can_vote? 
    @age >= 18 
  end
  # Destructive instance method 
  def reset_age!
    @age = nil
  end 
  # class methods with default values 
  def self.greet(name, informal=false, shout=false)
    greeting = "hi" if informal else "Hello" 
    if shout 
      "#{greeting} #{name}".upcase
    else 
      "#{greeting} #{name}"
    end
  end  
  # the same method with named parameters (supported by Ruby 2+)
  def self.greet(name, informal: false, shout: false)
    greeting = "hi" if informal else "Hello" 
    if shout 
      "#{greeting} #{name}".upcase
    else 
      "#{greeting} #{name}"
    end
  end 
end 
```
### Dynamic Typing 
Ruby is a dynamic langauge. Part of that means that no class definition is **ever** finalized; which means that we can re-open and add, remove or modify class behavior at **any** time. So if we want to add functionality to the `String` class, we can do so simply, like this: 
```rb
class String 
    def number_of_vowels
      gsub(/[^aeiou]/,'').size 
    end 
end 
```
This is commonly done in rails like so: 
```rb 
require 'active_support'
require 'active_support/core_ext/numeric'

# Returns the time as of 4 minutes prior to the execution of that line of code 
4.minutes.ago 
# => 2015-05-21 14:54:37 +0100 
``` 

### Duck Typing 
The idea here is that if "it walks like a duck, talks like a duck, then it must be a duck". Since Ruby is a dynamic langauge, class (and therefor object) definitions are **never** finalized; in other words, we can redefine class functionality at any time. 

This is best understood through an example. In the example below, I am defining a class (`EmptyClass`). This `EmptyClass` has no methods or attributes. I then "re-open" the super-class of all objects (`Object`) and give that a `ping` method, which returns `"pong"`. Now if I instantiate go back to `EmptyClass` and call `ping` again, you will see that that object now has a method (inherited from the super-class `Object`) and does **not** raise a `NoMethodError`. 
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

# Constants 

