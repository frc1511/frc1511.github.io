---
layout: page
title: Enumerations
nav_order: 6
parent: C++ Stuff
---

# Enumerations

* [Description](#description)

## Description

Enumerations are used to declare a custom type that can only have a specific set of values. They are useful for representing the state of a mechanism, or the available options for some function.

{% highlight cpp %}
enum MyEnum {
  OPTION_1,
  OPTION_2,
  OPTION_3,
};

/**
 * Instantiate a variable of type "MyEnum" named "myEnum" and set it to
 * OPTION_1.
 */
MyEnum myEnum = OPTION_1;
{% endhighlight %}

The values of a basic loosly typed enumeration (like the one above) can be implicitly converted to an integer. By default, the values of an enumeration start at `0` and increment by `1` for each value. The values of an enumeration can be explicitly set to any integer value.

{% highlight cpp %}
enum MyEnum {
  OPTION_1 = 1,
  OPTION_2 = 2,
  OPTION_3 = 3,
};

MyEnum myEnum = OPTION_1;

// "myInt" is now 1 (implicitly converted from "myEnum")
int myInt = myEnum;
// "myInt2" is now 2 (implicitly converted from "OPTION_2")
int myInt2 = OPTION_2;
{% endhighlight %}

Enumerations can also be strongly typed. This means that the values of the enumeration cannot be implicitly converted to an integer. This is useful for preventing bugs that could occur if the values of an enumeration were accidentally used as integers. Values of strongly typed enumerations also need to be accessed using the `EnumName::VALUE_NAME` syntax.

{% highlight cpp %}
enum class MyEnum {
  OPTION_1,
  OPTION_2,
  OPTION_3,
};

MyEnum myEnum = MyEnum::OPTION_1;

// "myInt" is now 0 (explicitly converted from "myEnum")
int myInt = static_cast<int>(myEnum);
{% endhighlight %}
