# Data Types

## Overview

Data types are fundamental to programming as they define the kind of data that can be stored and manipulated. Each data type has specific characteristics and operations associated with it. In this section, we will explore various data types commonly used in programming languages like Python.

## Types of Data
### Char
Represents a single character, such as 'A' or '1'. Char will typically use ASCII values to store characters. For example, the character 'A' is stored as 65 in ASCII. 

!!! Python 
    Python does not have a built-in char type; instead, it uses the string type to represent single characters. For example, 'A' is represented as a string with length 1.

### String
Represents a sequence of characters. In many languages, strings are mutable, meaning they can be changed after creation. 

!!! Python 
    In Python, strings are immutable. Examples include "Hello" or "123". Since Python 3.0 all `str` values support unicode using the [UTF-8](https://en.wikipedia.org/wiki/UTF-8){:target=_blank} encoding. A string can be in either single quotes (' ') or double quotes (" ").

### Boolean
Represents a logical value that can be either true or false. Boolean values are essential for decision-making in programming. 

!!! Python
    In Python, the `bool` type is used to represent boolean values. `True` and `False` are the only valid boolean values in Python.

### Integer
Represents whole numbers without a fractional component. Integers can be positive, negative, or zero. 

!!! Python
    In python, the `int` type is used to represent integers. Examples include 10 or -5.

### Real
Represents numbers with fractional components. Real numbers include both integers and floating-point numbers. 

#### Float
Represents floating-point numbers with a decimal point. Floats have a fixed precision and can be used for scientific calculations. 
!!! Python 
    In python, the `float` type is used to represent floating-point numbers. Examples include 3.14 or -0.5. 

#### Double
Represents double-precision floating-point numbers, providing higher precision than floats. 
!!! Python 
    In python, there are no built-in types for double precision floating point numbers. Instead, the `float` type is used to represent both single and double precision floating point numbers. 

## Type Casting
Type casting is the process of converting one data type into another. This can be done implicitly (automatically by the language) or explicitly (by the programmer). 
!!! Python
    In python, you can use the `int()`, `float()`, and `str()` functions to perform explicit type casting.



