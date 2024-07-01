#modules #ruby #load #require In Ruby, the concepts analogous to JavaScript's `import` and `export` (used in ES6 modules) are `require`, `require_relative`, and `load` for importing files, and the use of modules and classes to expose functionalities. Ruby doesn't have a direct counterpart to JavaScript's `export` statement, but it has different ways of organizing and accessing code across different files. Let's break these down:

### 1. `require`
- Used to include modules and libraries from Ruby's standard library or from installed gems.
- Can also be used to include other Ruby files.
- It loads the file only once, even if called multiple times.

```ruby
require 'json'
require './my_ruby_file'
```

### 2. `require_relative`
- Similar to `require`, but it allows you to load a file that is relative to the file containing the `require_relative` statement.
- Useful for referencing files within the same project structure without needing to specify the complete path.

```ruby
require_relative 'another_ruby_file'
```

### 3. `load`
- Loads and parses a file every time it's called, unlike `require` which does it only once.
- Generally used less frequently than `require` or `require_relative`.

```ruby
load 'some_file.rb'
```

### 4. Modules and Classes for Exposing Functionalities
- In Ruby, you typically define classes and modules in separate files. By `require`-ing a file, you gain access to its classes and modules.
- There's no explicit export statement; everything defined at the top level of a file (classes, modules, methods, etc.) is accessible after the file is required.

```ruby
# In file: my_module.rb
module MyModule
  def self.my_method
    puts "Hello!"
  end
end

# In another file
require './my_module'
MyModule.my_method  # => "Hello!"
```

### 5. Using Gems
- For larger and more complex libraries, Ruby uses gems, which are packaged libraries or applications.
- You include a gem in your project by adding it to your `Gemfile` and running `bundle install`, then using `require` to load it in your code.

### Summary
While Ruby's approach differs from JavaScript's ES6 module system, it provides a flexible way of managing dependencies and organizing code into reusable components. The `require` and `require_relative` statements are used to include files and libraries, and modules and classes are used to encapsulate and expose functionalities.#

In Ruby, `module`, `require`, and `load` are distinct concepts used for different purposes:

### Module
- **What It Is**: A `module` in Ruby is a way to group together methods, classes, and constants. It's primarily used for two reasons:
  - **Namespacing**: To prevent name clashes by creating a distinct namespace.
  - **Mixins**: To allow sharing functionality between classes, which is achieved by including or extending modules in classes.
- **Usage**: Defined with the `module` keyword, it cannot be instantiated like a class. Instead, it's included in classes or used as a namespace.
- **Example**:
  ```ruby
  module MyModule
    def module_method
      puts "Hello from the module!"
    end
  end

  class MyClass
    include MyModule
  end

  obj = MyClass.new
  obj.module_method  # Output: Hello from the module!
  ```

### Require
- **What It Is**: `require` is a method used to include external files and libraries in Ruby. It's primarily used to load and reuse code from other files.
- **Usage**: When you `require` a file, Ruby looks for it in its load path and loads it if it hasn't been loaded already. It's commonly used for including Ruby gems and other Ruby files.
- **Example**:
  ```ruby
  require 'json'  # Loads the JSON standard library
  require './my_library'  # Loads 'my_library.rb' from the current directory
  ```

### Load
- **What It Is**: `load` is similar to `require`, but it differs in how it includes files. It's another method to read and parse files in Ruby.
- **Usage**: Unlike `require`, `load` re-parses and re-loads the file every time it's called, even if it's the same file. This can be useful in development environments where files change frequently.
- **Example**:
  ```ruby
  load 'my_script.rb'  # Loads and executes 'my_script.rb'
  ```

### Key Differences
- **Modules (`module`)** are used within Ruby's code structure to encapsulate methods, classes, and constants, providing namespaces and mixins.
- **`require`** is a method for loading external files and libraries just once and is typically used to include functionality that your program needs to run.
- **`load`** also loads external files, but it does so every time the method is called, which can be useful for dynamically updating code in certain scenarios.

Understanding these distinctions is crucial for organizing Ruby code effectively and managing dependencies within your Ruby applications.

# Expanded #Ruby #Reference #Sheet

Sure, I'll expand the reference sheet to include more popular methods for Strings, Arrays, Hashes, Numbers, and Enumerable in Ruby:

```ruby
# Expanded Ruby Reference Sheet

# String Methods
str = "Hello World"
str.downcase             # "hello world"
str.upcase               # "HELLO WORLD"
str.capitalize           # "Hello world"
str.swapcase             # "hELLO wORLD"
str.length               # 11
str.strip                # Removes whitespace
str.lstrip               # Removes left whitespace
str.rstrip               # Removes right whitespace
str.include?("o")        # true
str.gsub("l", "r")       # "Herro Worrd"
str.sub("l", "r")        # "Herlo World"
str.split                # ["Hello", "World"]
str.split("")            # ["H", "e", "l", "l", "o", ..., "d"]
str.to_s                 # String representation
str.reverse              # "dlroW olleH"
str.chars                # ["H", "e", "l", "l", "o", ..., "d"]
str.empty?               # false
str.index("e")           # 1
str[0]                   # "H"
str[1,4]                 # "ello"
str.slice(1,4)           # "ello"
str * 2                  # "Hello WorldHello World"
str.chomp("d")           # "Hello Worl"
str.match(/lo/)          # MatchData "lo"
str.start_with?("He")    # true
str.end_with?("rld")     # true
str.count("l")           # 3
str.insert(5, " there")  # "Hello there World"

# Array Methods
arr = [1, 2, 3, 4, 5]
arr.push(6)              # [1, 2, 3, 4, 5, 6]
arr.pop                  # 6, [1, 2, 3, 4, 5]
arr.shift                # 1, [2, 3, 4, 5]
arr.unshift(0)           # [0, 2, 3, 4, 5]
arr.each { |x| puts x }
arr.map { |x| x * 2 }    # [4, 6, 8, 10]
arr.select { |x| x.even? } # [4]
arr.reject { |x| x.even? } # [3, 5]
arr.join("-")            # "2-3-4-5"
arr.reduce(:+)           # 14
arr.sort                 # [2, 3, 4, 5]
arr.uniq                 # Removes duplicates
arr.to_s                 # String representation
arr.min                  # Minimum value
arr.max                  # Maximum value
arr.sample               # Random element
arr.rotate(2)            # [4, 5, 2, 3]
arr.combination(2).to_a  # [[2, 3], [2, 4], [2, 5], ...]
arr.permutation(2).to_a  # [[2, 3], [2, 4], [2, 5], ...]
arr.zip(arr2)            # Combines two arrays
arr.flatten              # Flattens nested arrays
arr.include?(3)          # true
arr.find_index(3)        # Index of first occurrence
arr.delete_at(2)         # Delete element at index
arr.delete(3)            # Delete all occurrences
arr.clear                # []

# Hash Methods
hash = { a: 1, b: 2, c: 3 }
hash.keys                # [:a, :b, :c]
hash.values              # [1, 2, 3]
hash[:d] = 4             # { a: 1, b: 2, c: 3, d: 4 }
hash.delete(:a)          # Deletes key :a
hash.each { |k, v| puts "#{k}: #{v}" }
hash.each_key { |k| puts k }
hash.each_value { |v| puts v }
hash.has_key?(:b)        # true
hash.has_value?(3)       # true
hash.empty?              # false
hash.size                # 4
hash.to_s                # String representation
hash.invert              # { 1 => :a, 2 => :b, 3 => :c, 4 => :d }
hash.merge({ e: 5 })     # Combines hashes
hash.fetch(:b, "default") # 2
hash.store(:f, 6)        # Adds a new key-value pair
hash.key(3)              # :c
hash.value

?(2)           # true
hash.compact             # Removes nil values
hash.select { |k, v| v.even? }
hash.reject { |k, v| v.even? }
hash.transform_keys { |k| k.to_s }
hash.transform_values { |v| v * 2 }

# Number Methods
num = 10
num.even?                # true
num.odd?                 # false
num.next                 # 11
num.to_s                 # "10"
num.abs                  # Absolute value
num.zero?                # false
num.round                # Round number
num.ceil                 # Ceiling value
num.floor                # Floor value
num.digits               # [1, 0]
num.to_f                 # 10.0
num.positive?            # true
num.negative?            # false
num.times { |i| puts i } # 0 to 9
num.upto(15) { |i| puts i } # 10 to 15
num.downto(5) { |i| puts i } # 10 to 5
num.pred                 # 9
num.div(3)               # Integer division
num.modulo(3)            # Modulus
num.remainder(3)         # Remainder
num.gcd(5)               # Greatest common divisor
num.lcm(5)               # Least common multiple
num.between?(5, 15)      # Check if within range
num.sqrt                 # Square root
num ** 2                 # Square of number
```

This extended reference covers a wide range of methods, giving you a handy guide to some of the most commonly used functionalities in Ruby. Remember, the best way to get familiar with these methods is to use them in practice and consult the Ruby documentation for detailed explanations and additional methods.

#block #given 
In Ruby, a method can yield to a block provided with its call. This means you can execute a block of code from within the method. Here's a simple example to illustrate how to check if a block is given and then execute it:

### Example Method Definition

```ruby
def example_method
  if block_given?
    yield
  else
    puts "No block was given."
  end
end
```

### Usage

1. **Calling the Method Without a Block**:

```ruby
example_method
```

Output:

```
No block was given.
```

2. **Calling the Method With a Block**:

```ruby
example_method do
  puts "This is a block of code being executed."
end
```

Output:

```
This is a block of code being executed.
```

### Explanation

- The method `example_method` checks if a block is provided using `block_given?`.
- If a block is given, `yield` is called to execute the block.
- If no block is provided, it simply prints "No block was given."

This demonstrates how you can make your methods flexible and able to execute additional code passed in through blocks, enhancing the method's functionality dynamically based on the caller's needs.