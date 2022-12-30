---
layout: page
title: Statements
nav_order: 4
parent: C++ Documentation
---

# Statements

* [Description](#description)
* [Selection Statements](#selection-statements)
  - [If Statement](#if-statement)
  - [Switch Statement](#switch-statement)
* [Iteration Statements](#iteration-statements)
  - [While Statement](#while-statement)
  - [Do-While Statement](#do-while-statement)
  - [For Statement](#for-statement)
* [Jump Statements](#jump-statements)

## Description

Statements are the basic building blocks of a program. A statement is an instruction for the computer to execute to perform a specific task. A program can alter the flow of control by using statements such as selection statements, iteration statements, and jump statements to change the order in which statements are executed.

## Selection Statements
Selection statements are used to control whether or not a block of code is executed based on a condition.

### If Statement

The most basic selection statement is the `if` statement. The `if` statement evaluates a condition, and if the condition is true, the block of code inside the `if` statement is executed. If the condition is false, the block of code inside the `if` statement is skipped and the next statement is executed. If there is an `else if` following the `if`, the condition is evaluated and its block of code is executed if the condition is true. This process repeats for each `else if` statement. If there is an `else` following the `if` or `else if` and the conditions are all false, the block of code inside the `else` statement is executed.

{% highlight cpp %}
// --- If statement ---

// If x is greater than 0, then the block of code below is executed.
if (x > 0) {
  puts("x is positive.");
}

// --- If-else statement ---

// If x is greater than 0, then the block of code below is executed.
if (x > 0) {
  puts("x is positive.");
}
// If x is not greater than 0, then the block of code below is executed.
else {
  puts("x is not positive.");
}

// --- If-else-if statement ---

// If x is greater than 0, then the block of code below is executed.
if (x > 0) {
  puts("x is positive.");
}
// If x is equal to 0, then the block of code below is executed.
else if (x == 0) {
  puts("x is zero.");
}
// If x is less than 0, then the block of code below is executed.
else {
  puts("x is negative.");
}

// --- If statement with multiple conditions ---

// If x and y are both greater than 0, then the block of code below is executed.
if (x > 0 && y > 0) {
  puts("x and y are both positive.");
}
{% endhighlight %}

Sometimes you will see an `if` statement with just a single variable without any comparison operators. This checks if the variable is not equal to zero (i.e. `!= 0`). This is because the `if` statement checks if the condition is true, and any non-zero value is considered true. Since `false` is equal to zero, this is also a way to check if a boolean variable is `true` or `false`.

{% highlight cpp %}
// If x is not 0, then the block of code below is executed.
if (x) {
  puts("x is not 0.");
}

// If y is true, then the block of code below is executed.
if (y) {
  puts("y is true.");
}

// If z is false, then the block of code below is executed.
if (!z) {
  puts("z is false.");
}
{% endhighlight %}

### Switch Statement

The `switch` statement solves the same problem as the `if-else-if` statement, but it is easier to read and write. The `switch` statement evaluates an expression, and if the expression matches one of the cases, the block of code inside the case is executed. If the expression does not match any of the cases, the block of code inside the `default` case is executed. The `break` statement is used to exit each case in the `switch` statement.

{% highlight cpp %}
// Evaluate the value of x.
switch (x) {
  // If x is 0, the block of code below is executed.
  case 0:
    puts("x is 0.");
    break; // Exit the switch statement.
  // If x is 1, the block of code below is executed.
  case 1:
    puts("x is 1.");
    break; // Exit the switch statement.
  // If x is not 0 or 1, the block of code below is executed.
  default:
    puts("x is not 0 or 1.");
    break; // Exit the switch statement.
}
{% endhighlight %}

## Iteration Statements

Iteration statements are used to repeat a block of code a certain number of times or until a condition is met. Using iteration statements can reduce the amount of code you need to write.

### While Statement

The `while` statement is used to repeat a block of code until a condition is met. The condition is evaluated before the block of code is executed. If the condition is true, the block of code is executed. If the condition is false, the block of code is skipped and the next statement is executed.

{% highlight cpp %}
int x = 0;
// While x is less than 5, the block of code below is executed.
while (x < 5) {
  printf("x = %d\n", x); // Print the value of x.
  x++; // Increment x by 1.
}
{% endhighlight %}

### Do-While Statement

The `do-while` statement is similar to the `while` statement, but the condition is evaluated after the block of code is executed. This means that the block of code is always executed at least once.

{% highlight cpp %}
int x = 7;

// Even though x is not less than 5, the block of code below is executed.
do {
  printf("x = %d\n", x); // Print the value of x.
  x++; // Increment x by 1.
// While x is less than 5, the block of code above is executed.
} while (x < 5);
{% endhighlight %}

### For Statement

The `for` statement is used to repeat a block of code a certain number of times. The `for` statement contains three parts: the iterator variable initialization, the condition, and the iterator variable update. The iterator variable initialization is executed before the block of code is executed, and the condition is evaluated before the block of code is executed. If the condition is true, the block of code is executed. If the condition is false, the block of code is skipped and the next statement is executed. After the block of code is executed, the iterator variable update is executed, and the condition is evaluated again. This process repeats until the condition is false.

{% highlight cpp %}
/**
 * i is initialized to 0, the condition is evaluated, and the block of
 * code below is executed. When finished, i is incremented by 1, and
 * the condition is evaluated again. This process repeats until x is
 * not less than 5.
 */
for (int i = 0; i < 5; i++) {
  printf("i = %d\n", i); // Print the value of x.
}
{% endhighlight %}

## Jump Statements

Jump statements are used to change the order in which statements are executed. The `break` statement is used to exit a loop, and the `continue` statement is used to skip the rest of the current iteration of a loop.

{% highlight cpp %}
// Break statement.
for (int i = 0; i < 5; i++) {
  if (i == 3) {
    // Exit the loop.
    break;
  }
  printf("i = %d\n", i);
}

// Continue statement.
for (int i = 0; i < 5; i++) {
  if (i == 3) {
    // Skip the rest of the current iteration.
    continue;
  }
  printf("i = %d\n", i);
}
{% endhighlight %}