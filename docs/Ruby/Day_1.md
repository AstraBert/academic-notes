
> _This page is based on the official [Ruby quickstart](https://www.ruby-lang.org/en/documentation/quickstart/)_
## 1. Introduction to Ruby

Install Ruby for Ubuntu with:

```bash
sudo apt-get install ruby-full
```

And check the version with:

```bash
ruby -v
```

You can start an interactive shell:

```bash
irb #interactive ruby
```

## 2. Hello World and Maths

Write your first Hello World with

```ruby
puts "Hello World"
```

This function will return `=> nil`, which is the Ruby equivalent of python `None`

You can use also arithmetic operations such as:

```ruby
# sum
5+5
7-3
# multiplication
3*2
# power
3**2
# division
4/2
# other mathematical operations
Math.sqrt(9) # -> 3
Math.sin(3.14) # -> 0
```

## 3. Define methods 

Methods are the equivalent of functions in python:

```ruby
def hi
	puts "Hello world!"
end

# call the method:
hi()
```

You can also define parameters for a function:

```ruby
def hi(name)
	puts "Hello #{name}" # this is the Ruby way to do formatted strings
end
```

`name` can also be given a default value and/or capitalized:

```ruby
def hi(name = "clelia")
	puts "Hello #{name.capitalize}"
end

hi() # -> "Hello Clelia"
hi("chris") # -> "Hello Chris"
```

## 4. Define classes

Classes are not different in their syntax from python:

```ruby
class Greetings
	def initialize(name="World")
		@name = name # @ is like self in python
	end
	def say_hi
		"Hi #{@name}"
	end
	def say_bye
		"Bye #{@name}"
	end
end

# set the object as in python
greeter = Greetings("Pat")
```

But there is a core difference with python itself: you cannot get the attribute `name` unless you explicitly set it as an attribute inside the class. You can do it by actually modifying the class:

```ruby
# See all instance methods
Greetings.instance_methods
# See only the instance methods you defined
Greetings.instance_methods(false) # no ancestral methods
# Re-open and modify the class
class Greetings
	attr_accessor :name
end

# Check if the class responds to the name attribute
greeter = Greetings("Pat")

greeter.respond_to?("name") # get name
greeter.respond_to?("name=") # set name

# Set a new class object
greeter = Greetings.new("Andy")
# Set a new name
greeter.name = "Anne"
```

## 5. More advanced example

Let's take a look to an advanced example:

```ruby
#!/usr/bin/env ruby

class MegaGreeter
  attr_accessor :names

  # Create the object
  def initialize(names = "World")
    @names = names
  end

  # Say hi to everybody
  def say_hi
    if @names.nil?
      puts "..."
    elsif @names.respond_to?("each")
      # @names is a list of some kind, iterate!
      @names.each do |name|
        puts "Hello #{name}!"
      end
    else
      puts "Hello #{@names}!"
    end
  end

  # Say bye to everybody
  def say_bye
    if @names.nil?
      puts "..."
    elsif @names.respond_to?("join")
      # Join the list elements with commas
      puts "Goodbye #{@names.join(", ")}.  Come back soon!"
    else
      puts "Goodbye #{@names}.  Come back soon!"
    end
  end
end


if __FILE__ == $0
  mg = MegaGreeter.new
  mg.say_hi
  mg.say_bye

  # Change name to be "Zeke"
  mg.names = "Zeke"
  mg.say_hi
  mg.say_bye

  # Change the name to an array of names
  mg.names = ["Albert", "Brenda", "Charles",
              "Dave", "Engelbert"]
  mg.say_hi

mg.say_bye

  # Change to nil
  mg.names = nil
  mg.say_hi
  mg.say_bye
end
```

So:

- Arrays and lists have the same syntax as python (squared brackets)
- `if...else` syntax is similar to python, with `elsif` instead of `elif`
- Check if something is...
	- ...a null: `var.nil?`
	- ...a list: `var.respond_to?("each")` or `var.respond_to?("join")` (a list of strings, in the latter case)
-  Iterate over something with the `var.each do |var|...end` syntax: it's equivalent to `for var in vars` in python
- The `if __FILE__ == $0` is equivalent to the `if __name__ == "__main__"` in python and contains the "executable" part of the script

Execute the script with:

```bash
ruby script.rb
```

