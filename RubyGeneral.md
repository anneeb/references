# Ruby: General

## Basics

Comments
  Single line: # (until end of line)
  Multiple lines: =begin <br> body <br> =end
Output string with line break: puts "string"
Output string without line break: print
Access time: Time.now
  Access divisor: Time.now.divisor
Get user input without appending a new line: gets.chomp
Make ruby wait: sleep(seconds)
View object id: .object_id

## Variables

Define variable: variable = value
Multiple assignments: var1, var2 = val1, val2
Constants: use CAPS
Interpolation: #{variable}
Or equals: variable ||= value
  If variable is already assigned, keep variable, otherwise assign variable to value
Mutable: pass by value (integers, fixnums, floats, booleans)
Non-mutable: pass by reference (strings, arrays, hashes)

## Classes

Define class: thing.class
Strings: "text"
Booleans: true, false  
Numbers: fixnums (integers), floats (decimals)
  Convert to integer: .to_ i
  Convert to float: .to_f
Symbols: :symbol
Array: [object, object]
  Convert to array: (stuff).to_a
Hashes: {key => value, key => value}

## Classes As Objects

General
  Refer to the instance on which that method is being called: self
Creation and inheritance
  Create new class: class Name <br> body <br> end
  Inheritance: class Sub_class < Super_class <br> body <br> end
  Pass to superclass: super
Instance
  Instance method: def method <br> end
  Instance variables: @variable
    Define: object.instance_variable_set(:@variable, value)
Initialize
  Define: def initialize(argument) <br> @variable = argument <br> end
  Getter and setter: attr_accessor :method
Getters
  Define: def method <br> @variable <br> end
  Using attribute: attr_reader :method
Setters
  Define: def method=(argument) <br> @variable = argument <br> end
  Using attribute: attr_writer :method  
Class
  Class method: def self.method <br> body <br> end
    Refer to class: self
  Class variables: @@variable
Private
  Cannot be called by explicit receiver
  Private methods: private
Metaprogramming
  Calls the method name that is the key’s name, with an argument of the value (instance.key = value)
  Define: self.send("key=", value)

## Modules

General
  Collect and bundle a group of methods and make them available to any number of classes
  Define: module Name <br> body <br> end
  Access nested modules: parent::child
Adding module
  As instance methods: include Name
  As instance methods and override existing: prepend Name
  As class methods and override existing: extend Name

## Numerical Methods

General
  Print next fixnum: fixnum.next
  Random number with range: rand(range)
Algebraic
  Absolute value: num.abs
  Raise number to power: number ** power
  Square root: Math.sqrt(num)
Booleans
  Even or odd: num.even? and num.odd?
  Determine whether a number is prime: prime?(num)
Rounding
  Down to integer: num.floor
  Up to integer: num.ceil
  To n places after decimal: num.round(n)
LCM / GCM
  Least common multiple: receiver.lcm(argument or input)
  Greatest common divisor: receiver.gcd(argument or input)
Ranges
  Inclusive range: (start..end)
  Exclusive range: (start...end)

## Arrays

General
  Define: array = [object, object]
  Create empty array: Array.new(size, default)
  Return array length: array.length
  Reassign value by index: array[index] = value
  See if an element is part of an array: array.include?(element)  
Adding to an array (destructive)
  One item at the end (shovel): array << value
  Multiple items at the end: array.push("value", "value")
  One item at the beginning: array.unshift(value)
  At a given index: array.insert(index, value)
Removing from an array (destructive)
  Last item from the end or last n elements: array.pop(n)
  First item from the beginning or first n elements: array.shift(n)
  By argument: array.delete(argument)
  By index: array.delete_at(index)
Accessing an element
  By index: array[index]
    From the end: [-1] is last element, [-2] is penultimate, etc.
    Inclusive range: index1..index2 (includes index 2)
    Exclusive range: index1...index2 (excludes index 2)  
  First element: array.first
  Last element: array.last
  First n elements of the arrray: array.take(n)
  Remainder after n elements have been taken: array.drop(n)
  Smallest element: array.min
  Largest element: array.max
Cleaning up arrays (add ! for destructive)
  Remove duplicates from array: array.uniq
  Flatten nested arrays: array.flatten
  Remove nil elements from an array: array.compact
Rearranging arrays (add ! for destructive)
  Sort array by value: array.sort
    Explicit: array.sort do |a, b| <br> a <=> b <br> end
  Reverse order of an array: array.reverse
  Rotate array so that desired index becomes the first: array.rotate(index)
Joining arrays (concatenation)
  Destructive: array.concat(array)
  Non-destructive: array + array
  Return overlap: array & array
Analyzing arrays
  Return number of elements equal to argument: array.count(argument)
  Return first index of array where argument occurs: array.index(argument)
Changing data type
  Return array as string: array.inspect
  Convert array to string: array.join("separator")
  Array destruction: var1, var2 = [val1, val2]

## Strings

General
  Define: string = "string"
  Return string backwards: string.reverse
  Return length of string: string.size or string.length
Accessing by index
  Define: string[index]
  From the end: [-1] is last element, [-2] is penultimate, etc.
  Inclusive range: index1..index2 (includes index 2)
  Exclusive range: index1...index2 (excludes index 2)
Joining strings
  Destructive: string1 << string2
  Non-destructive: string1 + string2
Return string to array (non-destructive)
  By characters: string.chars
  With a specific delimiter: string.split("delimiter")
Case manipulation (add ! for destructive)
  Return string as lowercase: string.downcase
  Return string as uppercase: string.upcase
  Return string with first letter capitalized: string.capitalize
  Return string with cases swapped: string.swapcase
Analyzing strings
  Check if string is empty: string.empty?
  Check if string includes argument: string.includes?(argument)
  Check if string starts with argument: string.start_with?(argument)
  Return first index of string where argument occurs: string.index(argument)
  Return number of elements equal to argument: string.count(argument)
Remove characters from a string
  Destructive: string.delete!(argument)
  Non-destructive: string.delete(argument)
  White spaces (add ! for destructive): string.strip

## Hashes

General
  Define: hash = {key => value, key => value}
  Create a hash with default value: Hash.new(value)
  If keys are symbols: hash = {key: value, key: value}
  Adding to a hash: hash[key] = value
  Return number of key-value pairs: hash.length
  Convert hash to nested array: hash.to_a
  Join two arrays to make a hash: Hash[aray1.zip array2]
Accessing keys and values
  Accessing a value by key: hash[key]
  Return array with all keys: hash.keys
  Return array with all values: hash.values
  Return first key-value pair: hash.first
  Return the key-value pair with the lowest key: hash.min
Analyzing hashes
  Check if hash has key: hash.include?(key) or hash.key?(key) or hash.has_key?(key)
  Check if hash has value: hash.has_value?(value)
Sorting hashes into nested arrays
  By key: hash.sort_by {|key, value| key}
  By value: hash.sort_by {|key, value| value}
Iterators
  Each: hash.each {|key, value| body}
  Each key: hash.each_key {|key| body}
  Each value: hash.each_value {|value| body}
  Collect return values as a new array: .collect
Counter hashes
  Counts the number of occurrences of particular elements or types of elements within a collection
  Define: counter_hash = Hash.new(0)
  Using a counter hash within a function:
    object.each do |variable|
    counter_hash[variable] += 1

## Methods

General
  Define: def method(argument, argument) <br> body <br> end
  Declare method output: return output
Arguments
  Keyword: argument:
    Calling a method: method(argument: value, argument: value)
  Optional argument: argument = value

## Yield, Blocks, Procs, and Lambdas

Yield
  Define: yield(argument)
  Stops executing code in a method and executes code in a block
  With an argument: passes the argument into a block
Block
  Define: do <br> block <br> end or {block}
  Are not objects
Proc
  Define: variable = Proc.new {|argument| body}
  Execute: variable.call
  Can be assigned to a local variable
  More than one proc can be passed to a
  Returns nil for the missing argument, but do not throw an error
  Return immediately without going back to the caller
Lambda
  Define: variable = lambda {|argument| body} or variable = ->(argument) {body}
  Execute: (&variable)
  Expects and checks for a certain amount of arguments
  Return to the calling method, think of as anonymous functions

## Logic and Conditionals

Truthiness
  Determine if something is truthy: !!variable
  Truthy: numbers, strings, arrays, hashes
  Not truthy: nil, false
Boolean operators
  Not: !
  AND: &&
  OR: ||
  Comparison: ==
  Not equal: !=
  Greater than: >
  Less than: <
  Greater than or equal to: >=
  Less than or equal to: <=
  Spaceship operator: a <=> b
    Returns -1 if a < b
    Returns 0 if a = b
    Returns 1 if a > b
Control flow
  If statements: if condition <br> body <end>
  If / else statements: if condition <br> body <br> else <br> body <br> end
  If / else if / else statements: if condition <br> body <br> elsif condition <br> body <br> end
  Ternary operator: condition ? action_if_true : action_if_false
  Case statements: case variable <br> when value <br> action <br> else <br> action <br> end
Statement modifiers
  If: action if condition
  Unless: action unless condition

## Loops and Iterators

General
  Define: loop do <br> body <br> end
  Exiting a loop: break
  Counter: loop do <br> body <br> if counter condition <br> break <br> end <br> end
Times
  Run a block n times
  Define: n.times {block}
While
  Will keep executing while a condition is true
  Define: while condiiton <br> body <br> end
Until
  Will keep executing until a condition is true
  Define: until condition <br> body <br> end
For
  Will keep executing within a given range
  Define: for item in range <br> body <br> end
Iteration
  Will execute for each element in receiver
  Define: object.each do |variable| <br> body <br> end
  Define: object.each {|variable| body}
  To assess and reassign
    Arrays: use .each_index
    String: use .each_char
  Collect return values as a new array: .collect

## Enumerables

General
  Define: object.enumerable {|var| body}
  Passes each element in its receiver to a given block
All, none, and any
  Returns true if never returns falsey value: .all?
  Returns true if never returns truthy value: .none?
  Returns true if ever returns truthy value: .any?
Map / collect (add ! for destructive)
  Returns a collection that's the result of executing a block once for each element: .map or .collect
Count
  Returns the number of items that when passed to that block return a truthy value: .count
Delete If (destructive)
  Returns all items that return a truthy value and deletes them from the original collection: .delete_if
Select and reject (add ! for destructive)
  Returns collection containing all the elements that return a truthy value: .select
  Returns collection containing all the elements that return a falsey value: .reject
Find / detect
  Returns the first item that returns a truthy value: .find or .detect
Sort by (non-destructive)
  Returns collection by return values of elements when passed through a given block: .sort_by
Each with index and with index
  Iterate over a collection with item and item index: .each_with_index {|var, index| body}
  Add index variable to existing enumerable: .enumerable.with_index {|var, index| body}
  Add index variable with starting value to existing enumerable: .enumerable.with_index(value) {|var, index| body}
Reduce
  Returns collection as a single element
  With a symbol that names a binary method or operator: .reduce(:symbol)
  With a block and without an initial accumulator: .reduce {|acc, el| body}
    Where acc = accumulator and el = element
  With a block and with an initial accumulator: .reduce(initialAcc) {|acc, el| body}
    Where acc = accumulator and el = element
