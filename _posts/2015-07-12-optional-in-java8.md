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
The Optional class provides several instance methods to read the value contained by an Optional instance.

*get()*

The silplest way to get wrapped value from `Optional` by calling

{% highlight java %}
Person aPerson = optPerson.get();
{% endhighlight %}

You will get person object return if it present, but throws a `NoSuchElementException` otherwise. For thsi resaon I think it a bad idea to use `get()` to extract your object from Optional unless you’re really sure the optional contains a value.

*orElse(T other)*

This method allows you to provide a default value for when the optional doesn’t contain a value.

{% highlight java %}
Person aPerson = optPerson.orElse(anotherPerson);
{% endhighlight %}

From code above `optPerson` will return wrapped value if present otherwise return `anotherPerson`.

*orElseGet(Supplier<? extends T> other)*

`orElseGet(Supplier<? extends T> other)` is the lazy counterpart of the `orElse` method, because the supplier is invoked only if the optional contains no value. You should use this method either when the default value is time-consuming to create (to gain a little efficiency) or you want to be sure this is done only if the
optional is empty (in which case it’s strictly necessary).

{% highlight java %}
Person aPerson = optPerson.orElseGet(() -> expensiveCall());
{% endhighlight %}

From code above `expensiveCall()` will be executed if wrapped value in `optPerson` is not present.

*orElseGet(Supplier<? extends T> other)*

is similar to the get method in that it throws an exception when the optional is empty, but in this case it allows you to choose the type of exception that you want to throw.

{% highlight java %}
Person aPerson = optPerson.orElseThrow(() -> new SomeException("Some message"));
{% endhighlight %}

`SomeException` will throw if `optPerson` is empty.

*ifPresent(Consumer<? super T> consumer)*

lets you execute the action given as argument if a value is present; otherwise no action is taken.

{% highlight java %}
Person aPerson = optPerson.ifPresent(e -> {
    //some action with e
  });
{% endhighlight %}

#### References
- [Java 8 in Action](http://www.manning.com/urma/)
- [Java doc](https://docs.oracle.com/javase/8/docs/api/java/util/Optional.html)
