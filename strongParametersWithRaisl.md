## Rails & Strong Parameters

### Benefits:

1. Strong parameters allows you to perform both simple and complex validation
2. Strong parameters performs validation **before** the INSERT statement gets sent to the database

## Rails Validation

1. In the Model class, use the `validates` keyword to indicate the fields you want to perform validation on:

```rb
class City < ApplicationRecord
    # Here we are saying that we want to validate that when a new
    # model is created, it needs to include a value for `:name` and
    # a value for `:state` because we state that `presence:` = `true`
    validates :name, :state, presence: true
    # this does not care what the values are, as long as they are present
end
```

### Custom Validation Statement

Custom validation occurs after the controller processes the HTTP request. What I mean by this, is that we the corresponding controller

```rb
class City < ApplicationRecord
    validates :name, :state, presence: true # standard validation
    validates :crimes_per_capita, greater_than_zero # custom validation

    private

    # this is how we perform a custom validation
    # we can reference `self` to access the model created
    # by the controller.
    def greater_than_zero
        [:crimes_per_capita] < 0
    end
end
```

If we want to validate, and stop the INSERT statement from executing if our conditions are not met, we can use`thorw abort`:

```rb
class City < ApplicationRecord
    validates :name, :state, presence: true # standard validation
    validates :crimes_per_capita, greater_than_zero # custom validation

    private

    def greater_than_zero
        if self[:crimes_per_capita] < 0
            throw abort
        end
    end
end
```

Referencing an objects property can be done in two ways:

1. Dot Notation, using `self`

```rb
def greater_than_zero
    self.crimes_per_capita > 0
end
```

2. Object Notation

```rb
def greater_than_zero
    self[:crimes_per_capita] > 0
end
```
