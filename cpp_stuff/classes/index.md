---
layout: page
title: Classes
nav_order: 5
parent: C++ Stuff
---

# Classes

* [Description](#description)
* [Class Members](#class-members)
* [Class Usage](#class-usage)
* [Constructors and Destructors](#constructors-and-destructors)
* [Class Inheritance](#class-inheritance)

## Description

Classes are used to construct objects that contain data and functions. They are useful for organizing the robot program into logical units. Typically, each class represents a specific subsystem of the robot, however there are also classes that represent a utility or a specific task or action.

Classes are typically declared in a header file (.h) and defined in a source file (.cpp). The header file contains the basic information about what the class is and what functionality it provides; however, the actual implementation of the class's functions is written in the source file. This allows the header file to be included in multiple source files without causing a compiler error.

When a class is declared, a variable of that class type can be declared. This variable can be used to access the class's public data and functions.

## Class Members

Classes can contain [variables](/cpp_stuff/variables) and [functions](/cpp_stuff/functions). The access level of a class's members can be specified by declaring them under the `public` and `private` sections. If a variable or function is declared under the `public` section, it can be accessed from within the class and from outside the class. If a variable or function is declared under the `private` section, it can only be accessed from within the class. It is typically good practice to declare most members as `private` and only declare the members that need to be accessed from outside the class as `public`.

{% highlight cpp %}
// --- MyClass.h ---

class MyClass {
public: // Start of the public section.

  /**
    * Declares a function named "myPublicFunction" that can be accessed
    * from inside and outside the class.
    */
  void myPublicFunction();

private: // Start of the private section.

  /**
    * Declares a function named "myPrivateFunction" that can only be
    * accessed from inside the class.
    */
  void myPrivateFunction();

  /**
    * Declares a variable named "myPrivateVariable" that can only be
    * accessed from inside the class.
    */
  int myPrivateVariable;
};

// --- MyClass.cpp ---

#include "MyClass.h" // Include the header file for the class.

void MyClass::myPublicFunction() {
  printf("myPublicFunction! myPrivateVariable = %d\n", myPrivateVariable);
}

void MyClass::myPrivateFunction() {
  printf("myPrivateFunction! myPrivateVariable = %d\n", myPrivateVariable);
}
{% endhighlight %}

## Class Usage

The `MyClass` class can be used in other source files by declaring a variable of type `MyClass`:

{% highlight cpp %}
// Declare a variable of type "MyClass" named "myClass".
MyClass myClass;

// Call the "myPublicFunction" function.
myClass.myPublicFunction();

/**
 * ERROR: "myPrivateFunction" is a private function, so it cannot be
 * called from outside the class.
 */
myClass.myPrivateFunction();
{% endhighlight %}

## Constructors and Destructors

Sometimes it might be useful for a class to perform some initialization when it is created and some cleanup when it is destroyed. This can be accomplished by defining a constructor function and a destructor function, which are called when the class is created and destroyed, respectively. Constructors and destructors are special functions that can not be called directly. Neither the constructor or destructor functions have a return type. The constructor function may have parameters, but the destructor function cannot.

To declare a constructor function, the name of the class is used as the function name. To declare a destructor function, the name of the class is used as the function name, prefixed with a tilde (~). The constructor and destructor functions are typically declared in the public section of the class.

{% highlight cpp %}
// --- MyClass.h ---

class MyClass {
public:
  MyClass(int x); // Constructor function.
  ~MyClass(); // Destructor function.
};

// --- MyClass.cpp ---

#include "MyClass.h"

MyClass::MyClass(int x) {
  printf("MyClass was created! x = %d\n", x);
}

MyClass::~MyClass() {
  puts("MyClass was destroyed!");
}

// --- Other Source File ---

/**
 * Create a variable of type "MyClass" named "myClass" and call the
 * constructor function with the parameter "5".
 */
MyClass myClass { 5 };
{% endhighlight %}

## Class Inheritance

Classes can be derived from other classes. This allows a class to inherit functions and variables from another class. Derived classes work the same as normal classes, except that they can also access functions and variables from the base class. Base classes can contain `protected` members along with `public` and `private` members. `protected` members act as `private` members to the base class, but can be accessed by the derived class as `public` members.

{% highlight cpp %}
// --- BaseClass.h ---

class BaseClass {
public:
  void myPublicFunction();

protected:
  void myProtectedFunction();

private:
  void myPrivateFunction();
};

// --- DerivedClass.h ---

#include "BaseClass.h"

class DerivedClass : public BaseClass {
public:
  void myDerivedFunction();
};

// --- DerivedClass.cpp ---

#include "DerivedClass.h"

void DerivedClass::myDerivedFunction() {
  /**
   * OK: "myPublicFunction" is a public member of the base class.
   */
  myPublicFunction();

  /**
   * OK: "myProtectedFunction" is a protected member of the base class,
   * but can be accessed by the derived class as a public member.
   */
  myProtectedFunction();

  /**
   * ERROR: "myPrivateFunction" is a private member of the base class,
   * so it cannot be accessed by the derived class.
   */
  myPrivateFunction();
}
{% endhighlight %}

Base classes can declare `virtual` functions. A virtual function is a function that can be re-implemented (overriden) by the derived class. When a virtual function is called on an instance of the derived class, the function in the derived class is called instead of the function in the base class. The base class can also declare a pure virtual function. A pure virtual function is a function that has no implementation in the base class and must be implemented in the derived class (otherwise the derived class is also considered abstract and cannot be instantiated).

{% highlight cpp %}
// --- BaseClass.h ---

class BaseClass {
public:
  // A virtual function. Can be re-implemented in the derived class.
  virtual void myVirtualFunction();

  // A pure virtual function. MUST be re-implemented in the derived class.
  virtual void myPureVirtualFunction() = 0;
};

// --- DerivedClass.h ---

#include "BaseClass.h"

class DerivedClass : public BaseClass {
public:
  void myVirtualFunction() override;
  void myPureVirtualFunction() override;
};

// --- DerivedClass.cpp ---

#include "DerivedClass.h"

void DerivedClass::myVirtualFunction() {
  puts("myVirtualFunction was called!");
}

void DerivedClass::myPureVirtualFunction() {
  puts("myPureVirtualFunction was called!");
}
{% endhighlight %}