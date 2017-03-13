+++
comments = false
title = "Yet Another Equals x Hashcode Article"
date = "2014-07-11T10:54:24+02:00"
author = ""
menu = ""
image = "images/fingerprint.jpg"
tags = ["Java","Equals", "Hashcode"]
share = true
slug = "yet_another_equals_hashcode_article"
draft = false

+++

There are tons of articles about Java `equals()` and [hashcode()](https://en.wikipedia.org/wiki/Java_hashCode()) implementation. Why another one?

Lorem Ipsum Dolor Lorem Ipsum Dolor Lorem Ipsum Dolor Lorem Ipsum Dolor Lorem Ipsum Dolor Lorem Ipsum Dolor Lorem Ipsum Dolor Lorem Ipsum Dolor Lorem Ipsum Dolor Lorem Ipsum Dolor Lorem Ipsum Dolor Lorem Ipsum Dolor Lorem Ipsum Dolor Lorem Ipsum Dolor Lorem Ipsum Dolor Lorem Ipsum Dolor Lorem Ipsum Dolor Lorem Ipsum Dolor Lorem Ipsum Dolor Lorem Ipsum Dolor Lorem Ipsum Dolor Lorem Ipsum Dolor Lorem Ipsum Dolor Lorem Ipsum Dolor Lorem Ipsum Dolor Lorem Ipsum Dolor Lorem Ipsum Dolor Lorem Ipsum Dolor Lorem Ipsum Dolor Lorem Ipsum Dolor Lorem Ipsum Dolor 


Yep Yep

```
@Override
public int hashCode(){
    return Objects.hashCode(this.firstName, this.lastName);
}
```