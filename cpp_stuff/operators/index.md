---
layout: page
title: Operators
nav_order: 2
parent: C++ Stuff
---

# Operators

* [Description](#description)
* [Arithmetic Operators](#arithmetic-operators)
* [Relational Operators](#relational-operators)
* [Logical Operators](#logical-operators)
* [Bitwise Operators](#bitwise-operators)
* [Assignment Operators](#assignment-operators)
* [Increment and Decrement Operators](#increment-and-decrement-operators)
* [Ternary Operator](#ternary-operator)

## Description

Operators are used to perform operations on variables and values. Most operators are binary, meaning they take two operands. For most applications, operaters are used on variables with integral numeric types, however some exceptions exist when a custom type overloads the use of an operator.

## Arithmetic Operators

Arithmetic operators are used to perform arithmetic operations on variables and values. The following table lists the arithmetic operators:

NOTE: It is important to remember that the result of an operation depends on the types of the operands. For example, the result of `5 / 2` is `2`, but the result of `5.0 / 2` is `2.5`. In the first example, both operands are integers, so the result is an integer. In the second example, one operand is a floating-point number, so the result is a floating-point number.

* `+` - Addition
* `-` - Subtraction
* `*` - Multiplication
* `/` - Division
* `%` - Modulus (remainder)
  - This operator is only used with integers. It returns the remainder of the division of the two operands.
  - For use with floating-point numbers, use the `std::fmod(lhs, rhs)` function.

```cpp
int x = 5 + 5; // "x" is now 10

int y = (5 + 5) * 2 + 3; // "y" is now 23 (PEMDAS applies)

int z = 5 / 2; // "z" is now 2 (the decimal part is truncated because "z" is an integer)
double a = 5 / 2; // "a" is now 2.0 (the decimal part is truncated because "5" and "2" are integers, so the result of the division is an integer even though "a" is a double)
double b = 5.0 / 2; // "b" is now 2.5 (the decimal part is not truncated because "5.0" is a double, so the result of the division is a double)

int c = 5 % 2; // "c" is now 1 (5 divided by 2 is 2 with a remainder of 1)
double d = std::fmod(5.5, 2); // "d" is now 1.5 (5.5 divided by 2 is 2 with a remainder of 1.5)
```

## Relational Operators

Relational operators are used to compare two operands. The following table lists the relational operators:

* `==` - Equal to
* `!=` - Not equal to
* `>` - Greater than
* `<` - Less than
* `>=` - Greater than or equal to
* `<=` - Less than or equal to

```cpp
bool x = 5 == 5; // "x" is now true
bool y = 5 != 5; // "y" is now false
bool z = 5 > 5; // "z" is now false
bool a = 5 < 5; // "a" is now false
bool b = 5 >= 5; // "b" is now true
bool c = 5 <= 5; // "c" is now true
```

## Logical Operators

Logical operators are used to combine two or more conditions. The following table lists the logical operators:

* `&&` - Logical AND
* `||` - Logical OR
* `!` - Logical NOT

```cpp
bool x = true && true; // "x" is now true
bool y = true && false; // "y" is now false
bool z = true || true; // "z" is now true
bool a = true || false; // "a" is now true
bool b = !true; // "b" is now false
```

## Bitwise Operators

Bitwise operators are used to perform bitwise operations on variables and values. The following table lists the bitwise operators:

* `&` - Bitwise AND
* `|` - Bitwise OR
* `^` - Bitwise XOR
* `~` - Bitwise NOT
* `<<` - Bitwise left shift
* `>>` - Bitwise right shift

```cpp
int x = 5 & 3; // "x" is now 1 (5 in binary is 101, 3 in binary is 011, 101 & 011 is 001, which is 1 in decimal)
int y = 5 | 2; // "y" is now 7 (5 in binary is 101, 2 in binary is 010, 101 | 010 is 111, which is 7 in decimal)
int z = 5 ^ 3; // "z" is now 6 (5 in binary is 101, 3 in binary is 011, 101 ^ 011 is 110, which is 6 in decimal)
int a = ~5; // "a" is now -6 (5 in binary is 101, so ~5 is 010, which is 2 in decimal, and 2 in decimal is -6 in two's complement)
int b = 2 << 1; // "b" is now 4 (2 in binary is 10, so 2 << 1 is 100, which is 4 in decimal)
int c = 2 >> 1; // "c" is now 1 (2 in binary is 10, so 2 >> 1 is 1, which is 1 in decimal)
int d = 2 << 3; // "d" is now 16 (2 in binary is 10, so 2 << 3 is 10000, which is 16 in decimal)
```

## Assignment Operators

Assignment operators are used to assign values to variables. The following table lists the assignment operators:

* `=` - Assigns a value to a variable
* `+=` - Adds a value to a variable
* `-=` - Subtracts a value from a variable
* `*=` - Multiplies a variable by a value
* `/=` - Divides a variable by a value
* `%=` - Divides a variable by a value and assigns the remainder to the variable
* `&=` - Performs a bitwise AND operation on a variable and a value and assigns the result to the variable
* `|=` - Performs a bitwise OR operation on a variable and a value and assigns the result to the variable
* `^=` - Performs a bitwise XOR operation on a variable and a value and assigns the result to the variable
* `<<=` - Performs a bitwise left shift operation on a variable and a value and assigns the result to the variable
* `>>=` - Performs a bitwise right shift operation on a variable and a value and assigns the result to the variable

```cpp
int x = 5;
x += 5; // "x" is now 10
```

## Increment and Decrement Operators

Increment and decrement operators are used to increment or decrement a variable by 1. The following table lists the increment and decrement operators:

* `++` - Increments a variable by 1
* `--` - Decrements a variable by 1

```cpp
int x = 5;
x++; // "x" is now 6
x--; // "x" is now 5
```

The increment and decrement operators can be placed before or after a variable. If they are placed before a variable, the variable is incremented or decremented before the value is used. If they are placed after a variable, the variable is incremented or decremented after the value is used.

```cpp
int x = 5;
int y = ++x; // "x" is now 6 and "y" is now 6 ("x" is incremented before "y" is assigned the value of "x")
int z = x++; // "x" is now 7 and "z" is now 6 (the value of "x" is used before it is incremented)
```

## Ternary Operator

The ternary operator is used to choose a value based on a condition.

```cpp
int x = 5 > 3 ? 5 : 3; // "x" is now 5 (5 > 3 is true, so the value of "x" is 5)
int y = 5 < 3 ? 5 : 3; // "y" is now 3 (5 < 3 is false, so the value of "y" is 3)
```