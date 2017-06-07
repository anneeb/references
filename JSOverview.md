# Javascript: Overview

## Basics

Alert: alert()
Comments: // (same line) or */ and /* (within a line)
Data types:
  Primitive: number, "string", boolean (true/false), null, undefined, symbol
  Complex: object, array
  Define: typeof element
  Constructor: .constructor
Console: an object, will return "Object{}"
  Logging: console.log()
  Error: console.error()
  Warn: console.warn()
Debugger: debugger, opens debug console
This: refer to the thing it belongs to, reference Object
Create a copy of an object: Object.assign{{}, obj}

## Variables

Define: var a = 1, b = 2, ..., z = 26;
Reassign: a = 2
Non-reassignable: const a = b
Reassignable: let a = b, only within a block

## Arithmetic

Basic math
  Add: +
  Subtract: -
  Multiply: *
  Divide: /
Compound math
  var = var (operator) value
  Add: +=,
  Subtract: -=
  Multiply: *= (*)
  Divide: /=
Math and assignment
  Pre-crement: (operation)number, operated first, evaluated second
  Post-crement: number(operation), evaluated first, stored second
  Increment: number++
  Decrement: number--
  Modifiers: number (basic operation)= value, modifies variable
Parsing
  Integers: parseInt(string, base)
  Non-integers: parseFloat(string)
Math functions
  Create random number from 0 to 1: Math.random()
  Round number to integer: Math.floor()

## Flow-Control

Comparisons
  Equal: ===
  Less than: <
  Greater than: >
  Less than or equal to: <=
  Greater than or equal to: >=
  And: &&
  Or: ||
If/else and if/else if/else
  Define: if () {} else {}
  Define: if () {} else if () {} else {}
Ternary operator: if/else shortcut
  Define: condition ? valueIfTrue : valueIfFalse
Switch statement: large if/else if/else chain
  Define: switch (variable) {
    case a:
      break;
    case b:
      break;
    ...
    case z;
      break;
    default:
  }

## Strings

Interpolation: `string ${code}`
Return number or object as string: .toString()
Escape Sequences
  Single quote: \'
  Double quote: \"
  Back slash: \\
  New line: \n
  Carriage return: \r
  Tab: \t
  Backspace: \b
  Form feed: \f

## Arrays

General
  Define: var array = [element, element]
  Element: can be anything
  Access element: array[index]
  Sort array: array.sort()
Non-destructive
  Add to beginning: [element, ...array]
  Add to end: [array, ...element]
  Remove from beginning: array.slice()
  Remove from end: array.slice(0, array.length - 1)  
Destructive
  Add to beginning: array.unshift(element)
  Add to end: array.push(element)
  Remove from beginning: array.shift()
  Remove from end: array.pop()
  Add/remove to/from anywhere: array.splice(index, number to remove, elements to add)
Changing data types
  String to array: string.split("splitter")
  Array to string: array.join("connector")

## Objects

General
  Define: var object = {property: value, property: value}
  Property: can be strings
  Value: can be anything
  Access value: object.key or object[key]
  Check property: object.hasOwnProperty(property)
Constructors
  Object literal: var object = {}
  New keyword: var object = new Object()
  Constructor function: function object(value) {this.key = value;}
Non-destructive
  Add or update: Object.assign({}, object, {[key]: value})
  Delete: Object.assign({}, object, {[key]: undefined})
Destructive
  Add or update: object.key = value or object[key] = value
  Delete: delete object[key]

## Functions

Function declaration
  Define: var regular = function (){} or function regular(){}
  Invoke: regular()
  Name: regular.name = "name"
  Hoisted: yes
Function expression
  Define: var expression = function() {}
  Invoke: expression()
  Name: expression.name = undefined
  Hoisted: no
Arrow functions
  Define: var arrow = () => {}
  Invoke: arrow()
  Name: arrow.name = undefined
  Hoisted: no
  Contain the scope: yes

## Loops

For
  Define: for (initialization; condition; iteration) {}
  Example: for (var i = 0; i < 100; i++) {}
For-in
  Define: for (var prop in obj) {}
  Notes: iterates over the enumerable properties of an object in original insertion order
While
  Define: while (condition) {}
  Example: while (countdown > 0) {console.log(--countdown)}
  Notes: body will keep executing until the condition evaluates to false
Do-while
  Define: do {} while (condition)
  Notes: loop's body is executed at least once before the condition is tested
Exiting
  Break: immediately terminate a loop, does not return value
  Return: immediately terminates a function, returns value
  Continue: keeps going
For each
  Define: object.forEach(callback, argument)
  Callback: (element, index, list) => {}
  Argument: value to use as this (reference Object)

## Funciton STuff

Sleep with callback: window.setTimeout(callback, milliseconds)
Bind
  Def: function.bind(this, args) => function(args)
