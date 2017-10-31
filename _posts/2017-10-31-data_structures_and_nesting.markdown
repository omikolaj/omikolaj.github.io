---
layout: post
title:      "Data Structures and Nesting"
date:       2017-10-31 11:11:49 +0000
permalink:  data_structures_and_nesting
---

Understanding and becoming familiar with Ruby Data Structures can be daunting. It can seem especially difficult if you have never encountered the syntax and its length. When initially looking at deeply nested Data Structures, I had tough time distinguishing where the data began or ended and how to traverse them. However, just like with anything in coding and in life, the more you use it the better you understand it and become more efficient at it. 

In Ruby:

> "Arrays are ordered, integer-indexed collections of any object." - 
[https://ruby-doc.org/core-2.2.0/Array.html](http://)

For our purposes the keyword we should focus on in the array definition is *collections of any **object***. Object is key here because it represents a broad terminology allowing us to not only store primitive types such as integers or strings but also our custom types, such as class instances and even other arrays and *hashes*.

Examples of Arrays:
```
array = [1, 2, 3]
array_1 = ["Hello", 1, 3]
```
We can see that in Ruby arrays do not need to be type specific. We can put together a collection of different objects.

> "A Hash is a dictionary-like collection of unique keys and their values. Also called associative arrays, they are like Arrays, but where an Array uses integers as its index, a Hash allows you to use any object type." - [https://ruby-doc.org/core-2.4.2/Hash.html](http://)

Hashes can be thought of as dictionaries. Structure of a dictionary consists of a key and then following is the value. Key in a dictionary, being a unique word, and value its definition. In the same sense hashes allow us to create our own dictionary structures where we specify what the unique key and the corresponding value will be. This is referred to as *key value pairs*.

Examples of Hashes:
```
hash = {name: "Tim", hobby: "fishing", age: 23}
```

In the below example, is where I think Ruby Data Structures can become a little bit tricky to understand. We can have an array of hashes likewise we are allowed to have a hash that points to an array.
Example of a hash with an array as its value

```
people = { teachers: => ["Manny", "Marty" , "Moe"], students: => ["Tim", "Jon", "Grant"] }
```

If we needed to retrieve "Jon" from this hash we would need to specify the name of the hash and then the key and then the index of the value we want to retrieve:
```
people[:students][0]
#Tim
```

Here we have a key of the hash called *teachers* that points to a value pair that is an array consisting of string objects. There is nothing stopping us from creating an array of other arrays. Likewise, we can create a hash where its key is pointing to another hash:

Example of a hash nested inside another hash
```
schools = { :Greenbriar => {address:  "123 Main St", email: "school@abc.com", students: ["Jerry", "Gary" ,"Randy"] }
```

":Greenbriar" is the key and its value is another hash. There is no limit as to how deeply nested our Data Structures can go.

If we needed to retrieve student "Gary" we would do:
```
schools[:Greenbriar][:students][1]
#"Gary"
```

In the above example we have a hash called "schools" which has a key called "Greenbriar". The key "Greenbriar" points to a value of yet another hash. We can also see that this inner hash has keys for "address", "email" but it also has a key for "students" which points to an array as its value.

When working with Ruby deeply nested Data Structures, we can see it can easily get confusing and complicated. What makes it easier for me is "bubbling up". Basically moving up the chain from destination to the beginning. In the last example of the "schools" hash we could do following and find our nested piece of information.

Target is to retrieve "Gary". "Gary" is inside of an array. it is at index 1. The name of the array is students. *Noting students[1]*, then as we move up the chain, we see that students is a key inside the ":Greenbriar" hash. *Noting [:Greenbriar][:students][1].* Then in the last layer we see that ":Greenbriar" is the first key in the hash called schools thus our final statement would be schools[:Greenbriar][:students][1]. This is my personal flavor of tackling deeply Data Structures and what has helped expedite my understanding. 

