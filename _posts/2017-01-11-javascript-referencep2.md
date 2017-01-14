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

### Understanding Objects
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

#### Types of properties
Two types: data properties and accessor properties.

##### Data Properties
Contain a single location for a data value.  Have four attributes:
* `[[Configurable]]`: if true, may be redefined by removing the property via `delete`, changing the property's attributes, or changing the property into an accessor property.
* `[[Enumerable]]`: if true, property will be returned in a `for-in` loop.
* `[[Writable]]`: if true, the property's value can be changed.
* `[[Value]]`: contains actual data value for the property.

Use `Object,defineProperty()` to change the default property attributes.

###### Accessor properties
Do not contain a data value. Contain a getter and a setter function (both are not necessary). Have four attributes:
* `[[Configurable]]`: if true, may be redefined by removing the property via `delete`, changing the property's attributes, or changing the property into an accessor property.
* `[[Enumerable]]`: if true, property will be returned in a `for-in` loop.
* `[[Get]]`: the function to call when the property is read from. Default is `undefined`.
* `[[Set]]`: the function to call when the property is written to. Default is `undefined`.

Must use `Object.defineProperty()` to define an accessor property.

##### Defining Multiple properties
Use the `Object.defineProperties()` method to define multiple properties.

##### Reading Property attributes
Use `Object.getOwnPropertyDescriptor()` to retrieve the property descriptor for a property.  Arguments are the object and the name of the property to get. Returns an object with properties for `configurable`, `enumerable`, `get` and `set` for accessor properties or `configurable`, `enumerable`, `writable`, and `value` for data properties.

### Object Creation
#### Factory Pattern
Resolves issues associated with DRY and creating multiple instances of the same object. Does not address the issue of object identification.

```
function createPerson(name, age, job) {
    var o = new Object();
    o.name = name;
    o.age = age;
    o.job = job;
    o.sayName = function() {
        alert(this.name);
    };
    return o;
}
var person1 = createPerson("Shane", 44, "Junior Dev");
```

#### The Constructor Pattern
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
1. Create a new object.
2. Assign the `this` vale to the constructor to the new object.
3. Execute the code inside the constructor.
4. Return the new object.

When called with `new`, the resulting object has a `constructor` property that points back the the constructor function in created it.  

##### Constructors as Functions
Constructors are functions and, as such, differ from other functions only in the way they are used.

##### Problems with Constructors
One downside is the creation of methods in each instance. Defining methods in the constructor function means the same (but not identical) methods are created with every instance. You can get around this by pulling out the common methods and adding a property that points to the method(s) in the constructor. This pattern introduces clutter to the global scope with methods that only be used in relation to an object.  Thus, the prototype pattern.

#### The Prototype pattern
`prototype` property is an object that contains properties and methods that should be available to all instances of particular reference type.

```
function Person() {
}
Person.prototype.name = "Nicholas";
Person.prototype.age =29;
Person.prototype.job = "Doctor";
Person.prototype.sayName = function() {
    alter(this.name);
}
```

##### How Prototypes Work
When a function is created, it `prototype` property is also created with a property `constructor` that points back to the function on which it is a property. When a constructor is created it has an internal pointer to its prototype. This is `[[Prototype]]` which cannot be accessed by script.  Chrome, Safari and Firefox allows access through a property call `__proto__`.

Each instance of a constructor has internal properties that point back to to the prototype but no direct relationship to the constructor.

`Object.getPrototypeOf()` is valuable when you want to implement inheritance using the prototype.

Search for a property in an object starts at the instance of the object, continues up the prototype of the instance.

You can create a property on an instance with the same name as that on a prototype.  This does not replace the prototype version but, instead, shadows it (hides the prototype version from the instance).  Only `delete` can remove an instance version and restore the prototype link.

`hasOwnProperty()` can determine is if a property exists on an instance or prototype.

##### Prototypes and the in Operator
`in` can be used on its own and returns `true` when a property is accessible by the object (in the instance or its prototype). You can combine `hasOwnProperty()` and `in` to see if the property exists on the prototype.  

`in` can also be used in a `for-in` loop which access all properties that can be enumerated in the instance and the prototype. You can get a list of the enumerable properties of an object with `Object.keys()`.

`Object.getOwnPropertyNames()` returns all instance properties.

##### Alternate Prototype Syntax
You can use this syntax to support DRY when creating prototypes. This method does not include a constructor property as this method overwrites that is normally created when the instance is initialised. Adding `constructor` to the object literal resolves this issue.

You may also use `defineProperty()`.

```
function Person() {
}

Person.prototype = {
    constructor: Person,
    name: 'Shane',
    age: 44,
    job: 'Junior Dev',
    sayName: function() {
        alert(this.name);
    }
};
```

#### Dynamic Nature of Prototypes
Any changes made to a prototype are immediately reflected on all instances of that type. You cannot overwrite the entire prototype and expect the changes to a be available to all instances of that type.

#### Native Object Prototypes
All native reference types have their methods defined on the constructor's prototype. You can add methods to native prototypes although it is not recommended.  

#### Problems with Prototypes
The pattern negates the ability to pass initialisation arguments into the constructor, meaning that all instances get the same property value by default.

Main problem comes from shared nature.  A change from an instance to a prototype reference type will be reflected in all instances of the same prototype. So we combine the constructor and prototype patterns.

#### Combination Constructor/Prototype Pattern
Most common method for defining custom reference types. Constructor defines instance properties and the prototype pattern defines methods and shared properties.

#### Dynamic Prototype Pattern

```
function Person(name, age, job) {
    // properties
    this.name = name;
    this.age = age;
    this.job = job;

    // methods
    if (typeof this.sayName != "function") {
        Person.prototype.sayName = function() {
            alert(this.name);
        };
    }
}

var friend = new Person('Shane', 44, 'Junior Dev');
friend.sayName();
}

#### Parasitic Constructor Pattern
Fallback when other patterns fail. The same as the factory pattern except the function is called as a constructor. Should be not be used if other patterns work.

#### Durable Constructor Pattern
A _durable constructor_ is a constructor that follows a pattern similar to the parasitic constructor pattern, with two differences: instance methods do not refer to `this`, and the constructor is never called using the `new` operator.

```
function Person(name, age, job) {
    var o = new Object();

    o.sayName = function() {
        alert(name);
    };

    return o;
}
```

You cannot access the value of any variables in the returned object except through a method call.

### Inheritance
Implementation inheritance, where actual methods are inherited, is the only type supported by ECMAScript. Done through the use of prototype streaming.

#### Prototype Chaining
Primary method of inheritance. 
