---
title: C++ Operators
---

# Operators

## Description

Operators are used to perform operations on variables and values. Most operators are binary, meaning they take two operands. For most applications, operaters are used on variables with integral numeric types, however some exceptions exist when a custom type 'overloads' the use of an operator to perform a custom operation.

## Arithmetic Operators

Arithmetic operators are used to perform arithmetic operations on variables and values. The following table lists the arithmetic operators:

* `+` - Addition
* `-` - Subtraction
* `*` - Multiplication
* `/` - Division
* `%` - Modulus (remainder)
    - This operator is only used with integers. It returns the remainder of the division of the two operands.
    - For use with floating-point numbers, use the `std::fmod(lhs, rhs)` function.

!!! note
    The result of an operation depends on the types of the operands. For example, the result of `5 / 2` is `2`, but the result of `5.0 / 2` is `2.5`. In the first example, both operands are integers, so the result is an integer. In the second example, one operand is a floating-point number, so the result is a floating-point number.

```cpp
// "x" is 10
int x = 5 + 5;

// "y" is 23 (PEMDAS applies)
int y = (5 + 5) * 2 + 3;

// "z" is 2 (the decimal part is truncated because "z" is an integer)
int z = 5 / 2;

/**
 * "a" is 2.0 (the decimal part is truncated because "5" and "2" are
 * integers, so the result of the division is an integer even though
 * "a" is a double)
 */
double a = 5 / 2;

/**
 * "b" is 2.5 (the decimal part is not truncated because "5.0" is a
 * double, so the result of the division is a double)
 */
double b = 5.0 / 2;

// "c" is 1 (5 divided by 2 is 2 with a remainder of 1)
int c = 5 % 2;

// "d" is 1.5 (5.5 divided by 2 is 2 with a remainder of 1.5)
double d = std::fmod(5.5, 2);
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
bool y = 5 != 3; // "y" is now true
bool z = 5 > 3;  // "z" is now true
bool a = 3 < 5;  // "a" is now true
bool b = 5 >= 5; // "b" is now true
bool c = 3 <= 5; // "c" is now true
```

## Logical Operators

Logical operators are used to combine two or more conditions. The following table lists the logical operators:

* `&&` - Logical AND
* `||` - Logical OR
* `!` - Logical NOT

```cpp
bool x = true && true;  // "x" is now true
bool y = true && false; // "y" is now false
bool z = true || true;  // "z" is now true
bool a = true || false; // "a" is now true
bool b = !true;         // "b" is now false
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
unsigned char x = 0b0101 & 0b0011; // 0b0001
unsigned char y = 0b0101 | 0b0010; // 0b0111
unsigned char z = 0b0101 ^ 0b0011; // 0b0110
unsigned char a = ~0b0101;         // 0b11111010
unsigned char b = 0b0010 << 1;     // 0b0100
unsigned char c = 0b0010 >> 1;     // 0b0001
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
/**
 * "x" is now 6 and "y" is 6 ("x" is incremented before "y" is assigned
 * the value of "x")
 */
int y = ++x;

/**
 * "x" is now 7 and "z" is 6 (the value of "x" is used before it is
 * incremented)
 */
int z = x++;
```

## Ternary Operator

The ternary operator is used to choose a value based on a condition.

```cpp
// "x" is now 5 (5 > 3 is true, so the value of "x" is 5)
int x = (5 > 3) ? 5 : 3;

// "y" is now 3 (5 < 3 is false, so the value of "y" is 3)
int y = (5 < 3) ? 5 : 3;
```
