
# Getting an objects Public Methods 

Format: 

| Syntax | Example Text | Description | 
|:---|:---|:---| 
| ClassName | `User` | The name of the class you want to retrieve the public instance methods from | 
| `public_instance_methods` | `public_instance_methods` | Method inherited from object that returns the public methods of that class as an array |
| `methods` | `methods` | | 
| `grep` | `grep` | "grab" "read" "evaluate" print" | 

Code: 
```rb 
User.public_instance_methods.grep(/method_name/)
```