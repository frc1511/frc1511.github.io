---
layout: page
title: Functions
nav_order: 2
parent: C++ Stuff
---

# Functions

* [Description](#description)
* [Example 1 - Basic Function](#example-1---basic-function)
* [Example 2 - Function with Parameters](#example-2---function-with-parameters)
* [Example 3 - Function with Return Value](#example-3---function-with-return-value)

## Description

Functions contain a block of code that can be called from other parts of the program. Creating a function allows you to reuse code, and makes your code more readable and easier to maintain.

Functions are declared with a name, a return type, and a list of parameters.

## Example 1 - Basic Function

```cpp
void sayHi() {
  puts("Hi!"); // Prints "Hi!" to the console.
}
```
The function above is named "sayHi". It has no parameters, and it returns nothing (void). The function prints "Hi!" to the console when it is called, and then ends and returns to the calling function. Inside the function, the `puts()` function is called to print "Hi!" to the console. This transfers control away from the `sayHi()` function temporarily to print "Hi!", then returns control back to the `sayHi()` function after it is done printing. An example of calling this function is shown below:

```cpp
sayHi(); // Prints "Hi!" to the console.
```

## Example 2 - Function with Parameters

```cpp
void sayHiTo(std::string name) {
  printf("Hi, %s!\n", name.c_str()); // Prints "Hi, <name>!" to the console.
}
```
The function above is named "sayHiTo". It has one parameter, which is of type `std::string` and is named "name". The function returns nothing (void). The function uses its parameter "name" when it prints "Hi, \<name\>!" to the console. An example of calling this function is shown below:

```cpp
sayHiTo("Jeff"); // Prints "Hi, Jeff!" to the console.
```

## Example 3 - Function with Return Value

```cpp
int add(int a, int b) {
  return a + b; // Returns the sum of a and b.
}
```
The function above is named "add". It has two parameters, "a" and "b", which are both of type `int`. The function returns an `int` value, the sum of "a" and "b". An example of calling this function is shown below:

```cpp
int x = add(4, 2); // x is now equal to 6.
```
