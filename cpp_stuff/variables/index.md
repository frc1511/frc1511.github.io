---
layout: page
title: Variables
nav_order: 1
parent: C++ Stuff
---

# Variables

* [Description](#description)
* [Types](#types)
* [Type Conversion](#type-conversion)
* [Pointers & References](#pointers--references)
* [Type Qualifiers & Storage Class Specifiers](#type-qualifiers--storage-class-specifiers)

## Description

Variables are used to store data. They are declared with a name, a type, and a value.

## Types

Every variable must be assigned a type when it is declared. The type determines the size of the variable in memory, the range of values that can be stored in it, and the operations that can be performed on the variable. There are many different types of variables that you can use. These are some of the most common builtin types that you might come across:
* `int` - An integer. This is a whole number, such as 5 or -10.
  - `unsigned int` - An integer that can only be positive.
* `float` - A floating-point number. This is a number with a decimal point, such as 5.5 or -10.1.
  - `double` - A floating-point number with double the precision of a float (more decimal places).
* `bool` - A boolean value. This can be either `true` or `false` (technically, 1 or 0).
* `char` - A single character. This is a letter, number, or symbol, such as 'a' or '5' or '!'.
* `std::string` - A list of characters.
  - More information on strings can be found [here](https://en.cppreference.com/w/cpp/string/basic_string).
* `std::vector<int>` - A list of integers.
  - A `std::vector` can be used to represent a list of any type of variable. Just put the desired type of variable in the angle brackets when declaring it.
  - More information about vectors can be found [here](https://en.cppreference.com/w/cpp/container/vector).

Throughout the code we also use a number of custom types that we have created ourselves. These include [classes](/cpp_stuff/classes) and [enums](/cpp_stuff/enums/).

{% highlight cpp %}
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

// Declares a vector of integers named "myList" with the values 1, 2, 3, 4, and 5.
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
 * ERROR: Index 6 is out of bounds of the vector "myList", which only
 * has 5 elements.
 */
int z = myList.at(6);

// Adds the value 6 to the end of the vector "myList".
myList.push_back(6);
{% endhighlight %}

## Type Conversion

Sometimes, you might want to convert a variable from one type to another. In most situations, conversion is done automatically without any special syntax (implicit conversion). However, there are some cases where you need to explicitly convert a variable from one type to another (explicit conversion).

{: .important }
When converting a variable, make sure that the value of the variable can be represented in the new type. For example, if you have a variable of type `int` with the value -5, don't try to convert it to an `unsigned int` because an `unsigned int` can only be positive.

{: .note }
Data may be lost when converting from a type with more precision to a type with less precision. For example, converting a `double` to a `int` will result in the decimal part of the number being lost.

{% highlight cpp %}
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
{% endhighlight %}

## Pointers & References

Sometimes, you might want to pass a variable to a function, but you don't want to make a copy of it. Instead, you want to pass the variable itself so that the function can modify it. This is where pointers and references come in. A pointer is a variable that stores the memory address of another variable, not the actual value of the variable. A pointer is declared with an asterisk '\*' after the type of the variable it points to. To access the value of the variable that a pointer points to, you must use the dereference operator, which is also an asterisk '\*'.

{% highlight cpp %}
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
{% endhighlight %}

A reference is essentially the same thing as a pointer, except that it is declared with an ampersand '&' instead of an asterisk '\*', and it does not need to be dereferenced to access the value of the variable it points to.

{% highlight cpp %}
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
{% endhighlight %}

{: .warning }
Always be careful when using pointers and references. If you try to access a variable that a pointer or reference points to after the variable has been deleted or has gone out of scope, you will get undefined behavior and might crash your program. This is called a [dangling pointer](https://en.wikipedia.org/wiki/Dangling_pointer).

## Type Qualifiers & Storage Class Specifiers

Type qualifiers and storage class specifiers are used to modify the type of a variable. These are some of the most common type qualifiers and storage class specifiers that you might come across:
* `const` - Flags a variable as constant, meaning that it cannot be changed.
* `static` - Flags a variable as static, meaning that it will not be destroyed when the function it is declared in ends.

{% highlight cpp %}
// Declares a constant integer variable named "x" with the value 5.
const int x = 5;

// ERROR: Cannot change the value of a constant variable.
x = 10;

/**
 * Declares a static integer variable named "y" with the value 5.
 * This variable will not be destroyed when the function ends, so it
 * will still have the value 5 when the function is called again unless
 * it is changed later.
 */
static int y = 5;
{% endhighlight %}