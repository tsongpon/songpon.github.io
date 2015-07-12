---
layout: post
title: Optional in Java8
comments: true
---

## Problem with null
- It's source of error `NullPointerException` the most common Exception in Java, it happen when we use dot operator (.) with null reference.
- It bloats your code to prevent `NullPointerException` we have to have null check, it worsens readability.
- It’s meaningless it doesn’t have any semantic meaning, and in particular it represents the wrong way to model the absence of a value in a statically typed language.

## Introduce to Optional class
Java 8 introduce `java.util.Optional<T>`, a container object which may or may not contain a non-null value. We use this `Optional` to wrap the object that can be null so client can has a better way to handle with null able value.

#### Creating Optional objects

##### Empty Optional
You can create empty Optional object (Optional that contain nothing) by call static factory method `Optional.empty`

{% highlight java %}
Optional<Person> optPerson = Optional.empty();
{% endhighlight %}

##### Optional from none-null value
If you want to create Option from your object and you are 100% sure that your object is not null. You can use static factory method `Optional.of`

{% highlight java %}
Optional<Person> optPerson = Optional.of(person);
{% endhighlight %}

If `person` is `null` `NullPointerException` will be immediately thrown (rather than throw when client code try to use `person` in somewhere else)

##### Optional from null able value
If you want to create Optional that may cotain `null` value, you can call static factory method `Optional.ofNullable`

{% highlight java %}
Optional<Person> optPerson = Optional.ofNullable(person);
{% endhighlight %}

#### Extract value from Optional
