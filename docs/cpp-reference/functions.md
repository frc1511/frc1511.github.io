---
title: C++ Functions
---

# Functions

## Description

Functions contain a block of code that can be called from other parts of the program. Creating a function allows you to reuse code, and makes your code more readable and easier to maintain.

Functions are declared with a name, a return type, and a list of parameters.

## Example 1 - Basic Function

```cpp
void sayHi() {
  // Prints "Hi!" to the console.
  puts("Hi!");
}
```
The function above is named "sayHi". It has no parameters, and it returns nothing (void). The function prints "Hi!" to the console when it is called, and then ends and execution returns to the calling function. Inside the function, the `puts()` function is called to print "Hi!" to the console. This transfers control away from the `sayHi()` function temporarily to print "Hi!", then returns control back to the `sayHi()` function after it is done printing. An example of calling this function is shown below:

```cpp
// Runs the sayHi() function, which prints "Hi!" to the console.
sayHi();
```

## Example 2 - Function with Parameters

```cpp
void sayHiTo(std::string name) {
  // Prints "Hi, <name>!" to the console.
  printf("Hi, %s!\n", name.c_str());
}
```
The function above is named "sayHiTo". It has one parameter named "name", which is of type `std::string`. The function returns nothing (void). The function uses its parameter `name` to print "Hi, <name\>!" to the console when it is called, and then ends and execution returns to the calling function.

```cpp
// Runs the sayHiTo() function, which prints "Hi, Jeff!" to the console.
sayHiTo("Jeff");
```

## Example 3 - Function with Return Value

```cpp
int add(int a, int b) {
  // Returns the sum of a and b.
  return a + b;
}
```
The function above is named "add". It has two parameters, "a" and "b", which are both of type `int`. The function returns an `int` value, the sum of "a" and "b". An example of calling this function is shown below:

```cpp
/**
 * Runs the add() function and assigns its return value to the variable
 * "x", which is 6.
 */
int x = add(4, 2);
```
