---
layout: page
title: Statements
nav_order: 4
parent: C++ Stuff
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

```cpp
// If statement.
if (x > 0) { // If x is greater than 0, then the block of code below is executed.
  puts("x is positive.");
}

// If-else statement.
if (x > 0) { // If x is greater than 0, then the block of code below is executed.
  puts("x is positive.");
}
else { // If x is not greater than 0, then the block of code below is executed.
  puts("x is not positive.");
}

// If-else-if statement.
if (x > 0) { // If x is greater than 0, then the block of code below is executed.
  puts("x is positive.");
}
else if (x == 0) { // If x is not greater than 0, but is 0, then the block of code below is executed.
  puts("x is zero.");
}
else { // If x is not greater than 0 and is not 0, then the block of code below is executed.
  puts("x is negative.");
}

// If statement with multiple conditions.
if (x > 0 && y > 0) { // If x and y are both greater than 0, then the block of code below is executed.
  puts("x and y are both positive.");
}
```

Sometimes you will see an `if` statement with just a single variable without any operators. This checks if the variable is not equal to zero (i.e. `!= 0`). This is because the `if` statement checks if the condition is true, and any non-zero value is considered true. Since `false` is equal to zero, this is also a way to check if a boolean variable is `true` or `false`.

```cpp
int x = 5;
if (x) { // If x is not 0, then the block of code below is executed.
  puts("x is not 0.");
}

bool y = true;
if (y) { // If y is true, then the block of code below is executed.
  puts("y is true.");
}

bool z = false;
if (!z) { // If z is false, then the block of code below is executed.
  puts("z is false.");
}
```

### Switch Statement

The `switch` statement solves the same problem as the `if-else-if` statement, but it is easier to read and write. The `switch` statement evaluates an expression, and if the expression matches one of the cases, the block of code inside the case is executed. If the expression does not match any of the cases, the block of code inside the `default` case is executed. The `break` statement is used to exit each case in the `switch` statement.

```cpp
switch (x) { // Evaluate the value of x.
  case 0: // If x is 0, the block of code below is executed.
    puts("x is 0.");
    break; // Exit the switch statement.
  case 1: // If x is 1, the block of code below is executed.
    puts("x is 1.");
    break; // Exit the switch statement.
  default: // If x is not 0 or 1, the block of code below is executed.
    puts("x is not 0 or 1.");
    break; // Exit the switch statement.
}
```

## Iteration Statements

Iteration statements are used to repeat a block of code a certain number of times or until a condition is met. Using iteration statements can reduce the amount of code you need to write.

### While Statement

The `while` statement is used to repeat a block of code until a condition is met. The condition is evaluated before the block of code is executed. If the condition is true, the block of code is executed. If the condition is false, the block of code is skipped and the next statement is executed.

```cpp
int x = 0;
while (x < 5) { // While x is less than 5, the block of code below is executed.
  printf("x = %d\n", x); // Print the value of x.
  x++; // Increment x by 1.
}
```

### Do-While Statement

The `do-while` statement is similar to the `while` statement, but the condition is evaluated after the block of code is executed. This means that the block of code is always executed at least once.

```cpp
int x = 7;
do { // Even though x is not less than 5, the block of code below is executed.
  printf("x = %d\n", x); // Print the value of x.
  x++; // Increment x by 1.
} while (x < 5); // While x is less than 5, the block of code above is executed.
```

### For Statement

The `for` statement is used to repeat a block of code a certain number of times. The `for` statement contains three parts: the iterator variable initialization, the condition, and the iterator variable update. The iterator variable initialization is executed before the block of code is executed, and the condition is evaluated before the block of code is executed. If the condition is true, the block of code is executed. If the condition is false, the block of code is skipped and the next statement is executed. After the block of code is executed, the iterator variable update is executed, and the condition is evaluated again. This process repeats until the condition is false.

```cpp
for (int i = 0; i < 5; i++) { // x is initialized to 0, the condition is evaluated, and the block of code below is executed.
  printf("i = %d\n", i); // Print the value of x.
  // The iterator variable update is executed, and the condition is evaluated again.
}
```

## Jump Statements

Jump statements are used to change the order in which statements are executed. The `break` statement is used to exit a loop, and the `continue` statement is used to skip the rest of the current iteration of a loop.

```cpp
// Break statement.
for (int i = 0; i < 5; i++) { // x is initialized to 0, the condition is evaluated, and the block of code below is executed.
  if (i == 3) { // If i is 3, the block of code below is executed.
    break; // Exit the loop.
  }
  printf("i = %d\n", i); // Print the value of x.
  // The iterator variable update is executed, and the condition is evaluated again.
}

// Continue statement.
for (int i = 0; i < 5; i++) { // x is initialized to 0, the condition is evaluated, and the block of code below is executed.
  if (i == 3) { // If i is 3, the block of code below is executed.
    continue; // Skip the rest of the current iteration.
  }
  printf("i = %d\n", i); // Print the value of x.
  // The iterator variable update is executed, and the condition is evaluated again.
}
```