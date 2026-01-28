---
title: C++ Variables
---

# Variables

## Description

Variables are used to store data. They are declared with a name, a type, and a value.

## Types

Every variable must be assigned a type when it is declared. The type determines the size of the variable in memory, the range of values that can be stored in it, and the operations that can be performed on the variable. These are some of the most common types that you will come across in C++:

- `int` - An integer. This is a whole number, such as 5 or -10.
    - `unsigned int` - An integer that can only be positive.
- `float` - A floating-point number. This is a number with a decimal point, such as 5.5 or -10.1.
    - `double` - A floating-point number with double the precision of a float (bigger range, more precise).
- `bool` - A boolean value. This can be either `true` or `false` (technically, 1 or 0).
- `char` - A single character. This is a letter, number, or symbol, such as `'a'` or `'5'` or `'!'`.
- `std::string` - A list of characters.
    - More information on strings can be found [here](https://en.cppreference.com/w/cpp/string/basic_string).
- `std::vector<int>` - A list of integers.
    - A `std::vector` can be used to represent a list of any type of variable. Just put the desired type of variable inside the angle brackets.
    - More information about vectors can be found [here](https://en.cppreference.com/w/cpp/container/vector).

Throughout the robot code we also use a number of custom types that we have created ourselves. These include [classes](classes.md) and [enums](enums.md).

```cpp
// Declare an integer variable named "x" with the value 5.
int x = 5;
// Changes the value of "x" to 10.
x = 10;

// Declares a boolean variable named "b" with the value true.
bool b = true;

// Declares a string variable named "s" with the value "Hello, Ishan!".
std::string s = "Hello, Ishan!";

// Declares a character variable named "c" with the value 'a'.
char c = 'a';

/**
 * Declares a vector of integers named "myList" with the values 1, 2,
 * 3, 4, and 5.
 */
std::vector<int> myList = {1, 2, 3, 4, 5};

/**
 * Declares an integer variable named "y" with the value of index 0 of
 * the vector "myList", which is 1.
 */
int y = myList.at(0);

// Changes the value of index 0 of the vector "myList" to 10.
myList.at(0) = 10;

/**
 * Declares an integer variable named "myListSize" with the number of
 * elements in the vector "myList", which is 5.
 */
unsigned int myListSize = myList.size();

/**
 * "mylist" only has 5 elements (indexes 0 to 4), so trying to access
 * index 5 will cause an "out of range" error to be thrown at runtime.
 */
int z = myList.at(5);

// Adds the value 6 to the end of the vector "myList".
myList.push_back(6);
```

## Type Conversion (Casting)

Sometimes it is necessary to convert a variable from one type to another. In most situations, conversion is done automatically without any special syntax (implicit conversion). However, there are some cases where you need to explicitly convert a variable from one type to another (explicit conversion).

!!! Note
    When converting a variable, make sure that the value of the variable can be represented in the new type. For example, if you have a variable of type `int` with the value -5, don't try to convert it to an `unsigned int` because an `unsigned int` can only be positive. This will cause undefined behavior.

!!! note
    Data may be lost when converting from a type with more precision to a type with less precision. For example, converting a `double` to a `int` will result in the decimal part of the number being lost.

```cpp
int x = 5;
/**
 * Implicit conversion. Converted "x" from an int to a float. "y" is
 * now 5.0
 */
float y = x;

float z = 5.5;
/**
 * Implicit conversion. a is now 5 (the decimal part is truncated
 * because a is an integer).
 */
int a = z;

int b = -5;
/**
 * Implicit conversion from a signed integer to an unsigned integer.
 * This causes undefined behavior because b is negative, but c is
 * unsigned (can only be positive), so an "overflow" occurs, and the
 * value of c is now 4294967291.
 */
unsigned int c = b;

double d = 5.5;
/**
 * Explicit conversion. e is now 5 (the decimal part is truncated
 * because e is an integer). An explicit conversion was not necessary
 * here, but it improves readability and removes potential compiler
 * warnings.
 */
int e = static_cast<int>(d);

enum class MyEnum { A, B, C };
MyEnum f = MyEnum::A;
/**
 * Explicit conversion. g is now 0. This requires an explicit
 * conversion because MyEnum is a strongly typed enum, and the
 * compiler cannot implicitly convert it to an integer.
 */
int g = static_cast<int>(f);
```

## Pointers & References

A pointer is a variable that stores the memory address of another variable, not the actual value of the variable. Pointers are useful when you want to pass a variable to a function without making a copy of the variable, that way the function can modify the original variable.

Pointer types are declared with an asterisk `*` after the type of the variable it points to. To access the value of the variable that a pointer points to (dereferencing), you use the asterisk `*` before the pointer variable name. To get the memory address of a variable, you use the ampersand `&` before the variable name.

```cpp
// Declares an integer variable named "x" with the value 5.
int x = 5;

/**
 * Declares a pointer to an integer named "xPtr" that points to the
 * variable "x".
 */
int* xPtr = &x;

/**
 * Declares an integer variable named "y" with the value of the
 * variable "x", which is 5.
 */
int y = *xPtr;

// Changes the value of the variable "x" to 10.
*xPtr = 10;
```

A C++ 'reference' is essentially the same thing as a pointer, except that it is declared with an ampersand `&` instead of an asterisk `*` after the type of the variable it points to. References must be initialized when they are declared, and they behave like an alias for the variable they point to, which means no explicit dereferencing is needed to access the value of the variable. Any changes made to the reference will directly affect the original variable it points to

```cpp
// Declares an integer variable named "x" with the value 5.
int x = 5;

/**
 * Declares a reference to an integer named "xRef" that points to the
 * variable "x".
 */
int& xRef = x;

/**
 * Declares an integer variable named "y" with the value of the
 * variable "x", which is 5.
 */
int y = xRef;

// Changes the value of the variable "x" to 10.
xRef = 10;
```

!!! warning
    Always be careful when using pointers and references. [Dangling pointers](https://en.wikipedia.org/wiki/Dangling_pointer) and [null pointers](https://en.wikipedia.org/wiki/Null_pointer) are common sources of bugs in C++ programs.

## Type Qualifiers & Storage Class Specifiers

Type qualifiers and storage class specifiers are used to modify the type of a variable. These are some of the most common type qualifiers and storage class specifiers that you might come across:

- `const` - Makes a variable constant, meaning that it cannot be changed.
- `static`
    - For variables declared inside a function, makes the variable retain its value between function calls.
    - For variables declared outside a function, makes the variable have internal linkage, meaning that it can only be accessed from the same translation unit (source file).

```cpp
// Declares a constant integer variable named "x" with the value 5.
const int x = 5;

// Compiler error: Cannot change the value of a constant variable.
x = 10;

/**
 * Declares a static integer variable named "y" with the value 5.
 * This variable will not be destroyed when the function ends, so it
 * will still have the value 5 when the function is called again unless
 * it is changed later.
 */
static int y = 5;
```
