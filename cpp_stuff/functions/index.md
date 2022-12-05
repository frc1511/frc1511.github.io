---
layout: page
title: Functions
nav_order: 3
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

{% highlight cpp %}
void sayHi() {
  // Prints "Hi!" to the console.
  puts("Hi!");
}
{% endhighlight %}
The function above is named "sayHi". It has no parameters, and it returns nothing (void). The function prints "Hi!" to the console when it is called, and then ends and returns to the calling function. Inside the function, the `puts()` function is called to print "Hi!" to the console. This transfers control away from the `sayHi()` function temporarily to print "Hi!", then returns control back to the `sayHi()` function after it is done printing. An example of calling this function is shown below:

{% highlight cpp %}
// Runs the sayHi() function, which prints "Hi!" to the console.
sayHi();
{% endhighlight %}

## Example 2 - Function with Parameters

{% highlight cpp %}
void sayHiTo(std::string name) {
  // Prints "Hi, <name>!" to the console.
  printf("Hi, %s!\n", name.c_str());
}
{% endhighlight %}
The function above is named "sayHiTo". It has one parameter, which is of type `std::string` and is named "name". The function returns nothing (void). The function uses its parameter "name" when it prints "Hi, \<name\>!" to the console. An example of calling this function is shown below:

{% highlight cpp %}
// Runs the sayHiTo() function, which prints "Hi, Jeff!" to the console.
sayHiTo("Jeff");
{% endhighlight %}

## Example 3 - Function with Return Value

{% highlight cpp %}
int add(int a, int b) {
  // Returns the sum of a and b.
  return a + b;
}
{% endhighlight %}
The function above is named "add". It has two parameters, "a" and "b", which are both of type `int`. The function returns an `int` value, the sum of "a" and "b". An example of calling this function is shown below:

{% highlight cpp %}
/**
 * Runs the add() function and assigns its return value to the variable
 * "x", which is 6.
 */
int x = add(4, 2);
{% endhighlight %}
