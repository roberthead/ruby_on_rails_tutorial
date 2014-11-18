Southern Oregon University
Ruby on Rails Workshop
Robert Head
Co-founder, codingzeal.com
Nov 14, 2014

# Setting up your development environment

Getting ruby and Ruby on Rails set up on a new workstation can take some effort, especially on a Windows box. But if it hurts, we're probably doing it wrong, so let's do it the modern way, in the cloud!

Visit http://nitrous.io in a web browser

Fill out the sign up form ad click "Sign Up for Free"

Confirm your account via your email

Sign In

Click "Open Dashboard"

Fill out the "Create Your First Box" form and click "Create Box"

Wait for the box to provision and start.

Click "Next"

Read the introduction to Nitrous editing options and click "Okay, Take Me to my Box!"

You are now in the IDE (Integrated Development Environment) for the box.

Explore...

The IDE has the file structure on the left, a text editor in the middle, and a command-line terminal on the bottom. Everything we need!


# Introduction to Ruby

**Ruby** is a dynamic, reflective, object-oriented, general-purpose programming language. It was designed and developed in the mid-1990s by Yukihiro "Matz" Matsumoto in Japan.

The "killer app" for ruby has been rapidly developing Web applications in the Ruby on Rails framework.

## irb (interactive ruby shell)

Interactive Ruby Shell (irb) is a REPL (read-eval-print loop) console for programming in ruby.

From the command line at the bottom of your nitrous IDE:

    irb

### Use irb as a calculator

Jump right in and write some numerical expressions. For example:

    5 + 9
    5 - 7
    5 * 9
    5 / 3

Quirky! Integer division. Let's experiment.

    5 / 3.0
    5.0 / 3
    5 % 3

Exponent syntax

    5**3

### Calling Methods

In ruby, we call methods (functions) by appending a dot and the method name to an object like `object.method`

#### Method naming style

Method names are typically "snake case" (lower-case words separated by underscores. For example, this_is_snake_case)

Methods that return a boolean value usually have a question mark at the end.

    -99.abs
    57.even?
    57.odd?

### Strings

    "Some text"
    "fiz" + "bin"
    puts "fiz" + "bin"
    puts "Deep Space " + 9

Why did this fail?

    puts "Deep Space " + "9"

Strings can be single-quoted or double-quoted. Double-quoted strings "interpolate" ruby expressions that are inserted with the #{} syntax.

    'This will print just like it looks #{ 1 + 1 }'
    "Ten plus eight is #{ 10 + 8 }"

You can put any ruby expression you'd like inside #{} and it will insert the result as a String.

### Symbols

Symbols are string-like singleton objects, mostly useful as Hash keys. We'll get to Hashes soon!

We'll check the object_id to see that a given symbol, unlike a string, is always the same object in memory.

Style note: symbols are typically lower snake case, just like method names.

    :a
    :a.to_s
    "a".object_id
    "a".object_id
    "a".object_id
    :a.object_id
    :a.object_id

### Variables

Variables are typically snake case as well.

Assignment is done with a single equals sign.

    x = 99
    x / 9
    y = "foo"
    z = "bar"
    coder_nonsense = y + z

### More about methods

Almost everything in ruby is an object and responds to method calls. For example, every object responds to the 'class' method, which tells us what *type* the object is.

    53.class
    3.14.class
    "Salad".class
    :foo.class

Some methods have an exclamation point at the end of the name. By ruby convention, the ! usually indicates that it is dangerous or that it modifies the object. For example:

    s = "This is a String"
    s.upcase
    s
    s.update!
    s

### Arrays

    list = [42, 17, 23]

Accessing an element by index:

    list[0]
    list[1]
    list[2]
    list[3]
    list[-1]
    list[-2]

Some methods

    list.first
    list.last
    list.length
    list.sort
    list.sort.first
    list.class

### Even more about methods

Some methods accept or require one or more arguments. Let's call the join method on an Array object:

    ["Deep Space", 9].join
    ["Deep Space", 9].join(' ')

Parentheses are optional if the code is unambiguous without them.

    ["Deep Space", 9].join ' '

Want a crazy peek behind the curtain? Operators are actually just "syntactic sugar" for calling methods!

    5.+(4)
    51.* 3

#### Hashes

A Hash is also known as a Dictionary or an Associative Array in other languages. It collects key-value pairs.

    { :a => 1, :b => 2 }

Speaking ruby: The => symbol is called a "hash rocket"

Alternative syntax (looks exactly like JSON / Javascript)

    { a: 1, b: 2 }

Often the keys are symbols, but both the key and value can be any object

    { 'foo' => 45, 99 => 'baz' }

Hash values are accessed by key, similar to getting an Array element at a given index.

    h = { :name => "Jennifer Lawrence", :nickname => "J-Law", :known_for => "Hunger Games" }
    h[:name]
    h[:known_for]

However, Hashes are unordered, so you can't index them like an array.

    h[0]

...returns `nil` because there is no key 0.

#### Ranges

    r = 1..99
    r.include?(0)
    r.include?(1)
    r.include?(5)
    r.include?(5.5)
    r.include?(99)
    r.include?(99.1)
    r.to_a

### Conditionals and Flow

    5 == 3
    1 == 1.0
    "1" == 1

Let's put things together.

    x = rand(100)
    if x.odd?
      puts "#{x} is odd"
    else
      puts "#{x} is even"
    end

Confusify!

    puts "#{x = rand(100)} is #{x.odd? ? 'odd' : 'even'}"

Notice that we can do assignment inside interpolated expression within a String. Not readable, but shows very pithy!

### Looping and Blocks

    list = (0..10).to_a

Familiar syntax for newbies:

    for n in list
      puts n
    end

The ruby way to do something with each element of an Array:

    list.each do |n|
      puts n
    end

We put the behavior in a *block*, surrounded by do; end.

One-line blocks often use curly brace syntax instead of `do` and `end`

    list.each { |n| puts n }

There are other iterators. For example, `map` collects the results of the block

    squares = list.map { |n| n**2 }

###  Defining your own Classes

Ruby is an object-oriented language, so naturally we want to write our own classes.

    class Animal
      # constructor
      def initialize(name, noise)
        # instance variables being assigned to the argument values
        @name = name
        @noise = noise
      end
    end

    cat = Animal.new('Cat', 'Mrew!')
    cat.speak  # raises an exception because we didn't define this method

Want to add more functionality to the class? You can reopen any class any time!

    class Animal
      def speak
        puts "The #{@name.downcase} says '#{@noise}'"
      end
    end

    cat.speak

Even the existing object picked up the new behavior.

#### Inheritance

    class Dog < Animal
      def initialize
        super("Dog", "Woof!")
      end
    end

    dog = Dog.new
    dog.speak

#### Mixing Modules into a Class

Ruby has a singly-rooted inheritance hierarchy. If we want to "inherit" behavior from more than one place, we can organize behavior into modules.

    module Feedable
      def feed
        puts "The #{@name.downcase} eats. Grawm nom nom!"
      end
    end

    module Domesticated
      def pet
        puts "Aww, yeah. Right there... That's the spot."
      end
    end

    dog.eat

    class Animal
      include Feedable
    end

    class Dog
      include Domesticated
    end

    dog.feed
    dog.pet

    cat.feed
    cat.pet     # raises exception

Let's define a method directly to the cat object:

    def cat.pet
      puts "Aww, yeah. That's the sp... I WILL CUT YOU!!!"
    end

    cat.pet
    dog.pet

Neat. We're done with irb for now.

    exit


## Ruby Resources

Programming Ruby, a.k.a. the "Pickaxe" Book:
http://ruby-doc.com/docs/ProgrammingRuby/

Ruby for new coders:
https://pine.fm/LearnToProgram/

Ruby for the insane:
http://mislav.uniqpath.com/poignant-guide/

Searchable documentation for the ruby language
http://apidock.com/ruby

Get a head start doing _anything_ using 'ruby gems':
https://www.ruby-toolbox.com/


===================

# Introduction to Ruby on Rails

According to Wikipedia:

**Ruby on Rails**, or simply **Rails**, is an open source web application framework written in Ruby.

Rails is a full-stack framework that emphasizes the use of well-known software engineering patterns and paradigms, including convention over configuration (CoC), don't repeat yourself (DRY), the active record pattern, and model–view–controller (MVC).


## Creating a new Rails web application

From the nitrous.io IDE command-line console:

    cd workspace

    rails new blog

    cd blog

    bundle

    rails server

Select menu item: Preview > Port 3000

Your Rails app already responds to http requests!

Let's take a little tour of the structure of the project

  app/
  config/
  db/

## Git

Let's commit the code to a local git repository.

    git config --global user.name "John Doe"
    git config --global user.email johndoe@example.com
    git init
    git commit -am "Initial commit"

Enter your configuration and redo:

    git commit -am "Initial commit"


## User Stories

**User stories** are one way of defining what we want our application to do.

Let's make a blog!

### User Story #1: Creating Content

IN ORDER TO create content
AS bloggers
WE WANT to enter posts

    rails generate model Post header body:text

Look in db/migrate/

Look at db/schema.rb

    rake db:create

Look at db/schema.rb again

    rake db:migrate

Look at db/schema.rb again

Let's open a "rails console". It's just like irb, except we are in the context of our application.

    rails console

For inside the rails console, we can initialize and save a post

    post = Post.new
    post.header = "First!"
    post.body = "I would like to convey this message."
    post.save

Check that it's in the database:

    Post.count

Now let's make a web-based interface that non-coders can use to make blog posts.

Visit http://ruby-toolbox.com

Ruby Toolbox is a resource for finding **ruby gems**, which are libraries that provide functionality. We want an "admin interface" we can use to edit data. Look around in the Rails Admin Interfaces category. We'll choose rails_admin

In the IDE, open the file called Gemfile (it's in the root directory of the project)

Add this line at the bottom.

    gem 'rails_admin'

From the command line:

    bundle

    rails g rails_admin:install

Visit /admin

Holy crap!

    git add .

    git commit -am "Enable entry of posts"


### User Story #2: Reading Content

IN ORDER TO enjoy the content
AS readers
WE WANT to see blog posts

From the command line:

    rails g controller posts index show

Look at /app/controllers/posts_controller.rb

Look at /config/routes

Visit /posts

Restart server

Visit /posts again

Add fetch to index action

Flesh out the view template

Visit /posts

Commit our results

    git commit -am "Enable viewing of posts"


IN ORDER TO enable access control
AS legitimate bloggers
WE WANT to log in with accounts

  > rails generate model User name

  > rake db:migrate

  Look at db/schema.rb

  Visit ruby-toolbox.com and look up 'authorization'

  Add devise gem to Gemfile

  > bundle

  > rails generate devise:install

  Visit /

  Add root route to routes.rb

  Visit / again

  Add notice and alert stuff to layout.

  > rails generate devise User

  Look at new migration

  Visit /

  > rake db:migrate

  Visit / again

  Restart server

  Visit / again

  Visit /admin

  Look at fields added by devise and it's migration

  Create user

  > rake routes

  Add sign_in, sign_out, and sign_up to layout

  > git add .
  > git commit -m "Add log in"


IN ORDER TO protect the content
AS bloggers
WE WANT managing content to require login

  Add cancan to Gemfile

  > bundle

  > rails g cancan:ability

  Edit ability file

  Edit rails_admin config

  Boom!
