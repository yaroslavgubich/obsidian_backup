#classes #example #syntax #structure #oop 
___
#oop #scheme #blueprint 
#template
![[Pasted image 20240307194348.png]]

![[Pasted image 20240307194358.png]]
- Model: the `Recipe` class that defines the attributes of a recipe instance
- View: the interface of our app (`puts` & `gets`)
- Controller: the features of our app, the user actions

The #self  #keyword in #Ruby is a special variable that points to the object that is currently the context of the code being executed. Its meaning varies depending on where it is used:

1. **Inside Instance Methods**: Within an instance method, `self` refers to the instance of the class on which the method is called. It's used to access other instance methods and variables from within the current instance.

   ```ruby
   class MyClass
     def instance_method
       self.another_instance_method
     end

     def another_instance_method
       # Some code
     end
   end
   ```

   Here, `self` inside `instance_method` refers to an instance of `MyClass`, allowing it to call `another_instance_method`.

2. **Inside Class Methods**: When used inside class methods, `self` refers to the class itself, not to an instance of the class. This is useful for defining class-level variables or calling other class methods.

   ```ruby
   class MyClass
     def self.class_method
       self.another_class_method
     end

     def self.another_class_method
       # Some code
     end
   end
   ```

   `self` inside `class_method` refers to `MyClass`, making it possible to call `another_class_method`, which is also a class method.

3. **At the Class Level**: When `self` is used in the body of a class, outside of any method, it refers to the class itself. This is often seen when defining class methods, class variables, or using class macros (like `attr_accessor`).

   ```ruby
   class MyClass
     self.attr_accessor :my_attribute
   end
   ```

4. **In Singleton Methods**: When defining methods on individual objects (also known as singleton methods), `self` will refer to that specific object.

   ```ruby
   obj = Object.new
   def obj.singleton_method
     self
   end
   ```

   In `singleton_method`, `self` refers to `obj`, the object on which the method was defined.

Understanding the context in which `self` is used is crucial for correctly referencing methods, variables, and setting the scope of operation within Ruby classes and modules. It's a fundamental part of Ruby's object-oriented features, enabling objects to interact with themselves and invoke their own behaviors.
In Ruby, a super or parent class refers to a class that is inherited by another class, known as the subclass or child class. The concept of inheritance allows a subclass to inherit methods and attributes from its superclass, enabling code reuse and the establishment of hierarchical relationships between classes.

### Creating a Superclass

To create a superclass in Ruby, you simply define a class as you normally would. There is no special syntax for declaring a class as a superclass. What makes a class a "superclass" is the fact that another class chooses to inherit from it.

```ruby
class Vehicle
  def initialize(make, model)
    @make = make
    @model = model
  end

  def description
    "Make: #{@make}, Model: #{@model}"
  end
end
```

### Inheriting from a Superclass

To make a class a subclass of another, you use the `<` symbol followed by the name of the superclass when defining your subclass. This indicates that your subclass inherits from the specified superclass.

```ruby
class Car < Vehicle
  def initialize(make, model, doors)
    super(make, model) # Calling the superclass's initialize method
    @doors = doors
  end

  def description
    super + ", Doors: #{@doors}" # Enhancing the superclass's method
  end
end
```

### The `super` Keyword

The #super #keyword is used within a method to call a method of the same name in the superclass. This is particularly useful when overriding a method in the subclass but still wanting to use the logic of the overridden method from the superclass. The `super` keyword can be used in several ways:

- **`super` with no arguments**: Passes all the arguments received by the method from which it's called to the corresponding method in the superclass.
- **`super()` with empty parentheses**: Calls the corresponding method in the superclass without any arguments, regardless of what arguments were passed to the calling method.
- **`super` with specific arguments**: Allows you to specify which arguments to pass to the superclass method, giving you control over what data is sent to the superclass.

### Conclusion

In Ruby, the concept of superclasses and subclasses allows for the creation of hierarchical relationships between classes, enabling the reuse of code through inheritance. The `super` keyword plays a crucial role in this system, allowing subclasses to call methods from their superclass, either to utilize the superclass's implementation directly or to build upon it. This mechanism promotes DRY (Don't Repeat Yourself) principles and enhances code organization and readability.

In Ruby, a #super or #parent #class is a class that provides methods and attributes that can be inherited by another class, known as the subclass or child class. The mechanism of inheritance allows the subclass to use the functionality of the parent class, thereby promoting code reuse and reducing redundancy.

### How to Define a Parent Class in Ruby

Defining a parent class in Ruby is no different from defining any other class. You simply use the `class` keyword followed by the class name. Here is an example of a simple parent class:

```ruby
class Vehicle
  def initialize(make, model)
    @make = make
    @model = model
  end

  def start_engine
    "Engine of #{@make} #{@model} is starting."
  end
end
```

In this example, `Vehicle` is a parent class with an `initialize` method that takes two parameters (`make` and `model`) and a `start_engine` method that returns a string.

### How to Create a Subclass in Ruby

To create a subclass in Ruby that inherits from a parent class, you use the `<` symbol followed by the parent class's name. Here is how you can create a `Car` class that inherits from the `Vehicle` class:

```ruby
class Car < Vehicle
  def initialize(make, model, doors)
    super(make, model) # Calls the parent class's initialize method
    @doors = doors
  end

  def open_doors
    "Opening the #{@doors} doors of #{@make} #{@model}."
  end
end
```

In this subclass:

- The `initialize` method adds an additional parameter for `doors` and uses the `super` keyword to call the `Vehicle` class's `initialize` method with the `make` and `model` arguments. This ensures that the `@make` and `@model` instance variables are set by the parent class's constructor.
- The `Car` class also defines its own method, `open_doors`, which is specific to the `Car` class and not available in the `Vehicle` class.

### Conclusion

A super or parent class in Ruby is a foundational class that can be inherited by child classes to reuse code efficiently. Defining a parent class involves the same syntax as defining any class, while inheritance is achieved using the `<` symbol followed by the parent class name. The `super` keyword is particularly useful for calling methods in the parent class, allowing subclasses to extend or customize parent class functionality.

By leveraging inheritance, Ruby allows for the creation of well-organized, modular, and DRY (Don't Repeat Yourself) code, facilitating easier maintenance and extension of your applications.

#getters #setters  #ruby 
In Ruby, getters and setters are methods used to access and set the values of instance variables of a class. Ruby provides a convenient way to create these methods using `attr_reader`, `attr_writer`, and `attr_accessor`.

- **Getter Methods**: Allow you to retrieve or get the value of an instance variable.
- **Setter Methods**: Allow you to set or assign a value to an instance variable.

### Examples

#### Using `attr_accessor`

`attr_accessor` automatically creates both getter and setter methods for the specified instance variables.

```ruby
class Person
  attr_accessor :name

  def initialize(name)
    @name = name
  end
end

person = Person.new("Yaroslav")
puts person.name  # Getter method to retrieve the name
person.name = "Alex"  # Setter method to change the name
puts person.name
```

#### Using `attr_reader` and `attr_writer`

`attr_reader` only creates a getter method, and `attr_writer` only creates a setter method.

```ruby
class Person
  attr_reader :name  # Only a getter method for name
  attr_writer :name  # Only a setter method for name

  def initialize(name)
    @name = name
  end
end

person = Person.new("Yaroslav")
puts person.name  # Getter method to retrieve the name
person.name = "Alex"  # Setter method to change the name
puts person.name
```

### Conclusion

- **Getters and Setters** are used for accessing and setting instance variables in Ruby.
- **`attr_accessor`** creates both getter and setter methods.
- **`attr_reader`** and **`attr_writer`** are used when you only need a getter or a setter, respectively.
- These methods provide a way to encapsulate the data and promote better data handling within objects.
___

Here's a version that strikes a balance between detail and brevity:

```ruby
# Define a class named 'Dog'
class Dog
  # Constructor method: called when a new Dog instance is created.
  # Initializes the dog's name.
  def initialize(name)
    @name = name  # @name is an instance variable for storing the dog's name.
  end

  # Instance method: defines behavior for instances of the class.
  # This method allows a dog to "bark".
  def bark
    "#{@name} says Woof!"  # Returns a string of the dog barking.
  end

  # Class method: defines behavior on the class level, not instance level.
  # This method returns the species of the dog.
  def self.species
    "Canis familiaris"
  end
end

# Creating a new instance of Dog named "Buddy"
my_dog = Dog.new("Buddy")

# Calling instance method 'bark' on 'my_dog', outputs: Buddy says Woof!
puts my_dog.bark  

# Calling class method 'species' on 'Dog', outputs: Canis familiaris
puts Dog.species  
```

This version provides a balanced explanation for each part of the class, making it easier to understand the concepts of instance methods, class methods, and the purpose of `initialize`.

#attribute #reader 

. An attribute reader in Ruby is a method that returns the value of an instance variable. It provides a way to access the value of an instance variable from outside the class.

Ruby provides a convenient method `attr_reader` to automatically create these reader methods for specified instance variables, eliminating the need to manually define a method for each variable you wish to expose.

Here's an example to illustrate the use of `attr_reader`:

```ruby
class Person
  # Automatically create reader methods for name and age
  attr_reader :name, :age

  def initialize(name, age)
    @name = name
    @age = age
  end
end

# Create a new Person instance
person = Person.new("Alice", 30)

# Access the instance variables using the reader methods
puts person.name  # Output: Alice
puts person.age   # Output: 30
```

In this example, `attr_reader :name, :age` creates two methods, `name` and `age`, that return the values of the `@name` and `@age` instance variables, respectively. This allows you to access the `name` and `age` of the `person` object without directly accessing the instance variables, adhering to the principle of encapsulation.

#public and #private class functions in #ruby 


Yes, in Ruby, you can use the `private` and `public` keywords to specify the visibility of methods within a class. These keywords affect all subsequent method definitions in the class. Here's how you can use them:

- **Public Methods**: By default, all methods in a Ruby class are public unless explicitly made private or protected. You can also use the `public` keyword to make methods public if you need to change the visibility after defining some private or protected methods. Public methods can be called from anywhere.

- **Private Methods**: When you use the `private` keyword in a class, all method definitions that follow it are marked as private. Private methods cannot be called with an explicit receiver, meaning you cannot call a private method on an object (even within the same object). They are only accessible within the context of the current object.

Here's an example to illustrate both:

```ruby
class MyClass
  # This method is public by default
  def public_method
    puts "Public method called"
    private_method
  end

  private
  # This method is private
  def private_method
    puts "Private method called"
  end

  public
  # This method is public
  def another_public_method
    puts "Another public method called"
  end
end

my_object = MyClass.new
my_object.public_method
# Output: Public method called
#         Private method called

my_object.another_public_method
# Output: Another public method called

# Attempting to call the private method directly will result in an error
# my_object.private_method
# Error: private method `private_method' called for #<MyClass:0x000056...>
```

In this code, `public_method` and `another_public_method` are accessible from outside the `MyClass` instance, while `private_method` is only callable from within other methods of `MyClass`.

This flexibility allows you to design your classes with clear interfaces, separating the public interface (methods that can be called from outside the class) from the private implementation (methods that are intended to be used only within the class itself).\
#getters 

**getters** are instance methods allowing you to read or access an object’s **instance variables** values:

In Ruby, getters are methods used to access the value of an instance variable from outside the class. These methods provide a way to read the data encapsulated within an object, adhering to the principle of encapsulation in object-oriented programming. Encapsulation ensures that the internal representation of an object is hidden from the outside, only allowing access through well-defined interfaces.

For example, consider a class `Person` with an instance variable `@name`. To access the `@name` variable from outside the class, you would define a getter method:

```ruby
class Person
  def initialize(name)
    @name = name
  end

  # Getter method for @name
  def name
    @name
  end
end

person = Person.new("Alice")
puts person.name # Outputs: Alice
```

Ruby provides a convenient way to automatically create these getter methods using the `attr_reader` keyword:

```ruby
class Person
#getter
  attr_reader :name
  

  def initialize(name)
    @name = name
  end
end

person = Person.new("Alice")
puts person.name # Outputs: Alice
```

In this example, `attr_reader :name` automatically creates a getter method for the `@name` instance variable, allowing you to access its value with `person.name`.

To summarize, getters in Ruby are methods that allow you to retrieve the value of an instance variable from an object. Ruby's `attr_reader` provides a shortcut for defining these getter methods, making the code more concise and readable.


