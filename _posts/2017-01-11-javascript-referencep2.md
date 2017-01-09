---
layout: post
title: "JavaScript notes, part 2"
description: "A brief reference of basic JavaScript"
date: 2017-01-11
tags: [javascript, reference]
comments: true
share: true
---
# Basic JavaScript reference, p2

* TOC
{:toc}

## Object-Oriented Programming
Object-oriented (OO) languages use classes to create objects that have the same properties and methods.  ECMAScript (ES) does not have classes. Objects are different than in class-based languages.

ES objects are hash tables: key-value pairs where the value may be data or a function.

### Understanding Objects
Objects can be created using object literal notation:

```
var person = {
    name: 'Nicholas',
    age: 29,
    job: 'Software Engineer',
    sayName: function() {
        alert(this.name);
    }
};
```

#### Types of properties
Two types: data properties and accessor properties.

##### Data Properties
Contain a single location for a data value.  Have four attributes:
* `[[Configurable]]`: if true, may be redefined by removing the property via `delete`, changing the property's attributes, or changing the property into an accessor property.
* `[[Enumerable]]`: if true, property will be returned in a `for-in` loop.
* `[[Writable]]`: if true, the property's value can be changed.
* `[[Value]]`: contains actual data value for the property.

Use `Object,defineProperty()` to change the default property attributes.

###### Accessor properties
Do not contain a data value. Contain a getter and a setter function (both are not necessary). Have four attributes:
* `[[Configurable]]`: if true, may be redefined by removing the property via `delete`, changing the property's attributes, or changing the property into an accessor property.
* `[[Enumerable]]`: if true, property will be returned in a `for-in` loop.
* `[[Get]]`: the function to call when the property is read from. Default is `undefined`.
* `[[Set]]`: the function to call when the property is written to. Default is `undefined`.

Must use `Object.defineProperty()` to define an accessor property.

##### Defining Multiple properties
Use the `Object.defineProperties()` method to define multiple properties.

##### Reading Property attributes
Use `Object.getOwnPropertyDescriptor()` to retrieve the property descriptor for a property.  Arguments are the object and the name of the property to get. Returns an object with properties for `configurable`, `enumerable`, `get` and `set` for accessor properties or `configurable`, `enumerable`, `writable`, and `value` for data properties.

## Object Creation
### The Constructor Pattern
Constructors create specific types of objects. There are native constructors, such as `Object` or `Array`.  Customer constructors can be created.

```
function Person(name, age, job) {
    this.name = name;
    this.age = age;
    this.job = job;
    this.sayName = function() {
        alert(this.name);
    };
};

var person1 = new Person("Greg", 27, Doctor);
```

Constructor function names, by convention, start with a capital letter. Calling a constructor function with `new` causes four steps:
1 Create a new object.
2 Assign the `this` vale to the constructor to the new object.
3 Execute the code inside the constructor.
4 Return the new object. 
