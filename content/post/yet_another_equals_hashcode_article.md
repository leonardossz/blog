+++
comments = false
title = "Yet Another Equals x Hashcode Article"
date = "2017-04-21T00:00:00+02:00"
author = ""
menu = ""
image = "images/fingerprint.jpg"
tags = ["Java","Equals", "Hashcode"]
share = true
slug = "yet_another_equals_hashcode_article"
draft = false

+++

There are tons of articles about Java [equals and hashcode](https://en.wikipedia.org/wiki/Java_hashCode()) implementation. Why another one?

My first attempt: Because __almost every developer__ uses the automatic filling of `Object#equals(Object)` and `Object#hashCode()` through their favorite IDE without truly understanding its role within the application.

To make it more like a black box from JDK 7 onwards the programmer can just use the _Objects_ utility class like this:

```
@Override
public int hashCode(){
    return Objects.hash(firstName, lastName);
}
```

In an old post of [this blog](http://www.javaworld.com/article/2074301/core-java/java-7-objects-powered-compact-equals.html) someone wrote several _equals_ implementations demonstrating how useful the [Objects](https://docs.oracle.com/javase/8/docs/api/java/util/Objects.html#hash(java.lang.Object...)) class is, indeed.


In the [official JDK documentation](http://) you will find a set of conditions required to implement a consistent `equals(Object)` and `hashcode()`. Let's look into which one.

Keep in mind this very simple example:

```
public class SimpleAddress {
    private String streetName;
    private int houseNumber;

    public SimpleAddress(String streetName, int houseNumber) {
        this.streetName = streetName;
        this.houseNumber = houseNumber;
    }

    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (o == null || getClass() != o.getClass()) return false;
        SimpleAddress addressA = (SimpleAddress) o;
        return houseNumber == addressA.houseNumber &&
                Objects.equals(streetName, addressA.streetName);
    }

    @Override
    public int hashCode() {
        return Objects.hash(streetName, houseNumber);
    }
}
```

#### A good _equals_


As stated by _Oracle_ [here](https://docs.oracle.com/javase/8/docs/api/java/lang/Object.html#equals-java.lang.Object-):

1. __For any non-null reference value x, x.equals(null) should return false.__

	That's straight forward. No comments.

2. __It is _reflexive_: for any non-null reference value x, x.equals(x) should return true.__

	When you start to write your own code one of the first things you do is to _automagically_ let the IDE write `equals`, `hashCode` and `toString`. But does equality still hold when you update the class adding another field? The answer depends on each case. Here is a simple example: When you change your clothes does your identity, as a person, changes? (I hope you're not reading this on carnival ;) In most cases asking the IDE to regenerate the code method is harmless and advised.

3. __It is _symmetric_: for any non-null reference values x and y, x.equals(y) should return true if and only if y.equals(x) returns true.__

	Given that the instances of the classes can implement multiple interfaces the type check statement is very important for your sanity: ```if (o == null || getClass() != o.getClass()) return false;```. But nothing avoids that you just choose an object to be equal to a different type based on different field conditions, you'll just have to handle the type casting more carefully.

	This is weakest condition. Equality is established as a contract and nothing guarantees that two implementations of the same interface will agree on what is true thus you can end up with `x.equals(y)` different from `y.equals(x)`.

4. __It is _transitive_: for any non-null reference values x, y, and z, if x.equals(y) returns true and y.equals(z) returns true, then x.equals(z) should return true.__

	This is asserting that the implementation is reflexive and symmetric. 

5. __It is _consistent_: for any non-null reference values x and y, multiple invocations of x.equals(y) consistently return true or consistently return false, provided no information used in equals comparisons on the objects is modified.__

	The most important part is _..provided no information used in equals comparisons on the objects is modified._. That's it, if during runtime the objects changes the value of fields that is used to give the object's identity therefore the subsequent `equals` call can also change.


#### A good _hashCode_

This method is very important to keep the contract of _all hash based algorithms_ implementations of the JDK, like the `HashTable`. 

"In computing, a hash table (hash map) is a data structure which implements an associative array abstract data type, a structure that can map keys to values. A hash table uses a __hash function__ to compute an index into an array of buckets or slots, from which the desired value can be found. [Wikipedia](https://en.wikipedia.org/wiki/Hash_table)"

Here is the general contract:

1. __Whenever it is invoked on the same object more than once during an execution of a Java application, the hashCode method must consistently return the same integer, provided no information used in equals comparisons on the object is modified. This integer need not remain consistent from one execution of an application to another execution of the same application.__


	The [hash function](https://en.wikipedia.org/wiki/Hash_function) function __must not change__ the output if the fields used in the computation are the same.


2. __If two objects are equal according to the equals(Object) method, then calling the hashCode method on each of the two objects must produce the same integer result.__

	It's your duty to keep this contract. Nothing is enforced by the compiler, JDK nor the Virtual Machine.

3. __It is not required that if two objects are unequal according to the equals(java.lang.Object) method, then calling the hashCode method on each of the two objects must produce distinct integer results. However, the programmer should be aware that producing distinct integer results for unequal objects may improve the performance of hash tables.__

	As stated the integer value returned by `hashCode` is used as an index to store the object in an array of buckets/slots thus has to be a good [hash function](https://en.wikipedia.org/wiki/Hash_function) to disperse the data and try to avoid more than one object stored in the same bucket, a hash collision. 

	With a _perfect hash function_ each object is stored in exact one bucket leading to a [O(1)](https://en.wikipedia.org/wiki/Big_O_notation) time complexity to retrieve the data. However this perfection does not exist and collisions can happen, that's it, you can have two or more objects returning the same value for the `hashCode` implementation, this is not exactly a problem but can lead to poor performance when dealing with hash based collections.


### Conclusion

Whenever you have to put an _Object_ in a hash based collection implementation, mostly inheritances of the [Map](https://docs.oracle.com/javase/8/docs/api/java/util/Map.html) interface you may need to implement `hashCode` hence also `equals()` to keep the Java contract. 

I hope you can now have more understanding of the reasons or at least the right pointers to study more about the subject.