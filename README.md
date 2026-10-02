# Hiyoko

Hiyoko, named after the Japanese word for "chick", is a programming language designed for complete beginners.


:warning: Hiyoko is still Under Development.

:warning: Hiyoko is for beginners, but this document is written for experienced programmers.

## Language Design

Hiyoko aims to be **the easiest language** to learn programming and algorithms.  
The intended users of Hiyoko are those writing code for the first time.

Hiyoko helps users learn the basics of programming and smoothly transition to full-fledged languages like Python, JavaScript, C, Java and so on.  
To make this possible, Hiyoko has the following features:

- [Minimal Concepts](#minimal-concepts)
- [Minimal and common syntax](#minimal-and-common-syntax)

Hiyoko is designed solely for learning and has no practical use.

### Minimal Concepts

Popular programming languages today have many features and concepts due to their practicality.  
However, for complete beginners, this could be a hurdle.  
Even some basic programs include the concepts which might be difficult for beginners.

For example, you can write the most basic loop statement in Python like this:

**Python:**

```Python
for x in range(10):
  print(x)
```

The `range()` function returns an iterable object of the class named `range`.  
Learners, full of intellectual curiosity, might encounter the concepts of "Object" or "Class".  
Of course, all values in Python are objects, but is it necessary to know about for those who just want to loop `print(x)` 10 times for the first time?

In Hiyoko, the equivalent is as follows:

**Hiyoko:**

```JavaScript
for (var i = 0; i < 10; i = i + 1 ) {
    print(i);
}
```

This is also a familiar loop statement.
However, it requires more procedural thinking such as "adding `1` to `i` until condition `i < 10` becomes `false`".  
While this approach may seem more verbose, it can be understood with fewer concepts.  
Hiyoko believes that procedural programming is closer to the way humans usually think, much like the roots of our programming languages today.

Another example is that Hiyoko does not perform implicit type conversion.  
The following code in JavaScript can be written due to implicit type conversion or having multiple equality operators ( `==` and `===`).

**JavaScript:**

```JavaScript
let x = 1;

if(x == "1") {
    console.log(x); // 1
}
```

This might confuse beginners learning about the concept of data type, or make them unaware of their mistakes.

In Hiyoko, the equivalent outputs "Type error".

**Hiyoko:**

```JavaScript
var x = 1;

if(x == "1" /* Type Error */) {
    print(x);
}
```

All operators in Hiyoko require operands with the same data types.  
This inconvenience will remind learners that each value has its own data type.

### Minimal and Common syntax

Hiyoko has the most basic data types and control structures.  
Please refer to [Language Overview](#language-overview) section.

## Language Overview

### Statement

The program consists of statements.  
A statement that does not have a block **always** ends with `;`.

```JavaScript
42; // Expression statement

var x; // Variable declaration statement

// Function declaration statement
func foo() {
    return "foo"; // Return statement
}

// If statement
if (true) {
    doSomething();
} // Do not end with `;`
```

Hiyoko has a block statement:

```
{}
```

There is no empty statement unlike JavaScript:

```JavaScript
; // SyntaxError
```

### Data types, Literal expression, and Operators

#### Integer

```JavaScript

// Common binary operators are supported
((2 + 3) * 5 - 7 / 11) % 13; // 12
0 < 0; // false
0 >= 0; // true

7 / 11; // 0

// Unary plus and minus
-+1; // -1
```

#### Float

:warning: Under Development

#### Boolean

```JavaScript
true && false; // false

// The latter `false` is not evaluated (short-circuit evaluation)
true || false; // true

```

#### String

```JavaScript
"Hello, " + "World!"; // Hello, World!
```

#### Array

```JavaScript
// Index starts at 0
[1, 2, 3][2]; // 3

// Index must be a non-negative value of Integer type
[1, 2, 3][-1]; // Index error

// Any data type element can be held
[1, 2, 3, ["foo", true, []]][3][2]; // []

// Mutable
var arr = [1, 2, 3];
push(arr, 4);
arr; // [1, 2, 3, 4]
```

#### None

```JavaScript
none; // Represents the absence of a value, whether it is intentional or not
```

### Variable Declaration and Scope

#### Declaration

Variable declaration **always** requires the explicit `var` keyword.
This is intended to make learners aware of the necessity of defining a variable when they need to retain a value.

```JavaScript
var x = 1;

// Reassignment
x = 2;

// Redeclaration
var x; // Without initialization, `none` is assigned

```

There is only **one keyword** `var` to declare variables.  
There is no way to declare a constant value.

#### Scope

`var` declares a variable with block scope, so all variables in Hiyoko have block scope.

```JavaScript
{
    var x = 10;
    {
        x; // 10
    }
}
x; // Name error * This is not JavaScript!
```

### Control Structures

Hiyoko is not expression-oriented.  
These are statements and return no value.

#### If Statement

```JavaScript
if (age <= 3) {
    price = 100;
} else if (3 < age && age <= 9) {
    price = 300;
} else {
    price = 500;
}
```

Curly braces are always required.

```JavaScript
if (true) doSomething(); // Syntax error
```

#### For Statement

```JavaScript
for (var i = 0; i < 100; i = i + 1) {
    if (i % 2 == 0 ) {
        continue;
    }
    odd_sum =  odd_sum + i;
}
```

`break` statement can also be used in for statement.

Curly braces are always required.

```JavaScript
for (;;) ; // Syntax error
```

#### While Statement

```JavaScript
while (x < 100) {
    x = x + 1;
    if (x % 2 == 0) {
        continue;
    }
    odd_sum = odd_sum + x;
}
```

`break` statement can also be used in while statement.

Curly braces are always required.

```JavaScript
while (true) ; // Syntax error
```

### Function Declaration and Call Operator

Functions cannot be treated as "first-class" citizens.  
There is no explicit function data type or literal expressions for them.

```JavaScript
// Declaration
func add(x, y) {
    return x + y;
}

// Function call
add(1, 2);
```

```JavaScript
// Function without a return statement
func myPrint(s) {
    print(s);
}

myPrint("Hello, Hiyoko!");
```

#### Lexical scope

Like many other languages, free variables in functions are statically resolved.

```JavaScript
var y = 1;
func add(x) {
    return x + y; // `y` is a free variable
}
add(2); // 3
```

There is no concept of hoisting, unlike JavaScript.

```JavaScript
add(1, 2); // Name error

func add(x, y) {
    return x + y;
}
```

### Built-in functions

#### print()

```JavaScript
print("Hello, World!"); // Print "Hello, World!" to standard output
```

#### len()

```JavaScript
var arr = [1, 2, 3];
len(arr); // 3

```

```JavaScript
len("foo"); // 3
```

#### push()

```JavaScript
var arr = [1, 2, 3];
push(arr, 4); // [1, 2, 3, 4]
```

#### pop()

```JavaScript
var arr = [1, 2, 3];
pop(arr); // 3
arr; // [1, 2]
```
