---
layout: post
title: "JavaScript notes"
description: "A brief reference of basic JavaScript"
date: 2016-12-08
tags: [javascript, reference]
comments: true
share: true
---
# Basic JavaScript reference

* TOC
{:toc}

## Reference Types
### Objects

* most used type in JavaScript
* limited functionality
* ideal for storing and transmitting data around an application

#### Creating objects

* use the `new` with constructor `Object`
* object literal notation `{ }` (the preference of most developers)

#### Accessing object properties

* dot notation: `object.property`
* bracket notation: `object['property']`

Both will return the value of the property.

### Array type
An array is an ordered list that contain any data type on each slot.  This is unique to Javascript.

* dynamically sized

#### Creating arrays

* use the `new` with `Array` constructor (`new Array()` or `new Array(20)`)
* use array literal notation `[]`

#### Getting and setting values

Use square brackets and provide the zero-based numeric index of the value. The number of items is stored in the `length` property. `length` can be used to change the size of an array: `array.length = 2` creates (or changes) an array with length 2.

#####  Adding with `length`

* `array[array.length] = 'item'` adds an item to the array at the end
* can add 4,294,967,295 items

##### Detecting an array
```
if (Array.isArray(value)) {
    // do something on the array
}
```

#### Conversion Methods

* `toString()` and `valueOf()`: returns comma-seperated string of array values
* `toLocaleString()`: may return same as `toString()` and `valueOf()`
* `join`: can specify the separator

#### Stack Methods
An array object can act just like a stack, which is a _first-in-last-out_ structure.

* insertion: `push`
* removal: `pop`

#### Queue Methods
A structure that restricts access in a _first-in-first-out_ structure.

* removal of first item: `shift`
* insertion at front of array: `unshift`

#### Reordering Methods

* `reverse`: reverses the items in an array
* `sort`: sorts the items of an array smallest to largest. Can pass a comparison function.
** accepts two arguments and returns a negative number if the first argument should come before the second, a zero if the arguments are equal, or a positive number if the first argument should come after the second.
* both reordering methods return a reference to the array on which they were applied.

#### Manipulation Methods

* `concat`: creates a new array based on all of the items in the current array; copies the array and then appends the method arguments to the end and returning the newly constructed array.
* `slice`: creates an array that contains one or more items already contained in an array. Takes two arguments - where to start and where to stop.
* `splice`: used to insert items into the middle of an array
** deletion: two arguments, where to start and how many to delete `splice(0, 2)`. Returns an array that contains the items were returned.
** insertion: inserting to a specific position by providing three or more arguments: the starting position, the number of items to delete, and the item(s) to insert. `splice(2, 0, "red")`
** replacement: inserting into a specific position while simultaneously deleting items by specifying three arguments: starting position, the number of items to delete, and any number of items to insert.

#### Location Methods

* `indexOf`: starts at the beginning and proceeds to end.
* `lastindexOf`: starts from the last item in the array and continues to the front.

Both accept two arguments: the item to look for and an optional index from which to start looking. The methods return the position of the item in the array or -1 if the item does not exist.

#### Iterative Methods

Five methods that accept two arguments: a function to run on each item and an optional scope object in which to run the function. The function passed into one of these three methods will receive three arguments: the array item value, the position of the item in the array, and the array object itself. The methods do not change the array.

* `every()`: runs the function on every item in the array and returns `true` if the function returns `true` for every item.
* `filter()`: runs the function on every item in the array and returns an array of all items for which the function returns `true`.
* `forEach()`: runs the function on every item in the array.  No return value
* `map()`: runs the function on every item and returns the result of each function call in an array.
* `some()`: runs the function on every item and return `true` if the function returns `true` for any one item.

#### Reduction Methods

Both methods iterate over all items in the array and build up a value that is ultimately returned. Each accepts two arguments: a function to call on each item and an optional value upon which the reduction is based.

* `reduce()`: starts at first item. Used to perform operations such as adding all numbers in an array.
* `reduceRight()`: starts at last item.

The function passed into the methods accepts four arguments: the previous value, the current value, the item's index, and the array object.

### The Date Type

`Date` type stores dates as number of milliseconds that have passed since midnight on January 1, 1970 UTC.

`var now = new Date()`

To create a date passed in the millisecond representation of the date, use `Date.parse()` or `Date.UTC()`.

* `Date.parse()` accepts string representing the date. Passing a string automatically runs `Date.parse()`. Supports:
** month/date/year
** month_name data, year
** day_of_week month_name date year
** ISO 8601 extended format YYYY-MM-DDTHH:mm:ss:sssZ (only ECMAScript 5)
* `Date.UTC()` accepts year, zero-based month, the day of the month, and the hours, minutes, seconds, and milliseconds of the time. Year and month are required. Date and time created in the local time zone, not GMT.
* `Date.now()`: produces the millisecond representation when the method is run.

#### Inherited Methods
* `Date.toLocaleString()`: returns the date and time in a format appropriate for the locale in which the browser is being run.
* `Date.toString()`: date and time with time-zone information.

Should only use for debugging - not display.
* `Date.valueOf()`: returns millisecond representation so one can compare dates.

#### Date-formatting Methods

* `toDateString()`: displays the date's day of the week, month, day of the month, and year. Inconsistent display.
* `toDateString()`: shows the date's hours, minutes, seconds and time zone in implementation and local-specific format.
* `toLocaleDateString()`: displays the date's hours, minutes, and seconds in an implementation-specific format. Inconsistent display.
* `toUTCString()`: shows the complete UTC date.

#### Date/Time Component Methods

* `getTime()`: millisecond representation; same as `valueOf()`.
* `setTime(milliseconds)`: sets the millisecond representation, changing the date.
* `getFullYear()`: return four-digit year.
* `getUTCFullYear()`: returns four-digit year of UTC value.
* `setUTCFullYear(year)`: set the year of the UTC date.
* `getMonth()`: gets zero-based month.
* `getUTCMonth()`: returns zero-based month of UTC date.
* `setMonth()`: sets month starting at zero. Greater than 11 add years.
* `getDate()`: return the day of the month.
* `getUTCDate()`: day of UTC date.
* `setDate(date)`: sets the day. if higher than number of days in month, increases month.
* `setUTCDate(date)`: same as above for UTC date.
* `getDay()`: return the date's day of the week, zero-based starting with Sunday.
* `getUTCDate()`: same as above for UTC date.
* `getHours()`: return date's hours between 0 and 23.
* `getUTCHours()`: same for UTC date.

These repeat for minutes, seconds and milliseconds.

* `getTimezoneOffset()`: returns the number of minutes that the local timezone is offset from UTC. Sensitive to Daylight Savings Time.

### The RegExp Type
Supports regular expressions.  
```var expression = /pattern/flags;```

The pattern part can be any simple or complicated regular expression. Each expression can have zero or more flags.  Three supported flags are:
* `g`: indicated global mode, applying all of a string.
* `i`: case-insensitive mode.
* `m`: multi-line mode.

```
var pattern1 = /at/g;
var pattern2 = /\[bc]at/i;
var pattern3 = /.at/gi;
```
##### Metacharacters
`( [ { \ ^ $ | } ] ) ? * + .`

Must be escaped by `\` to be used as part of an expression.

##### RegExp constructor

Expressions can be created using `RegExp`. Takes two arguments: the expression and any flags.
```
var pattern2 = new RegExp("[bc]at", "i");
```

### The Function Type
Functions are objects with function names being pointers. Defined using function-declaration syntax:
```
function sum (num1, num2) {
    return num1 + num2;
}
```
or a function expression:
```
var sum = function(num1, num2) {
    return num1 + num2;
};
```
#### Function Declarations versus Function Expressions
Declarations are read and available in an execution context before any code is executed, whereas function expressions aren't complete until the execution reaches that line of code.

Declarations are made available through _function declaration hoisting_.

#### Functions as Values
Functions can be passed into another function as an argument and return a function as the result of another function.

#### Functions Internals
Functions have three objects, `arguments`, `this` and `caller`.
* `arguments`: array-like object that contains arguments passed to the function.
** `arguments.callee`: contains the function name that owns the arguments.  Can be used to decouple calling a function recursively from its name.
* `this`: reference to the context object that the function is operating on.
* `caller`: reference to the function that called a function or `null` if called from global scope.

#### Function Properties and Methods
Functions have properties and methods. Two properties:
* `length`: indicates the number of named arguments that the function expects.
* `prototype`: the actual location of all instance methods for reference types.
* `apply()` and `call()`: call the function with a specific `this` value, setting the value of the `this` object inside the function body.
* `bind`: creates a new function instance whose `this` value is bound to the value that was passed into `bind()`.

### Primitive Wrapper Types
Every time a primitive value is read, an object of the corresponding primitive wrapper type is created behind the scenes allowing access to any number of methods for manipulating the data. Applies to `boolean`, `string` and `number` types.

#### The Boolean Type
You can create a `boolean` type with the `new` constructor. Be careful when using this instance in code. For example:
```
var falseObj = new Boolean(false);
var result = falseObj && true;
alert(result); // true

var falseValue = false;
result = falseValue && true;
alert(result); // false
```
It is recommended not to use `Boolean` object.

#### The Number Type

* `toFixed()`: string of number with a specified number of decimal points (0-20).
* `toExponential()`: string of number in e-notation.
* `toPrecision()`: returns either fixed or exponential representation of a number, whichever makes the most sense.  Recommended method. Decimal places 1 through 21.

The same issues related to `Boolean` types apply to `Number` in that primitive `typeOf` will return `number` but `Number` will evaluate to object.

#### The String Type

##### Character Methods
* `charAt()`: returns character at the given position. In ECMAScript 5, `[]` returns character.
* `charCodeAt()`: returns character ascii code at the given position.

##### String-manipulation Methods
Create a new string from a string.
* `concat()`: concatenates one or more strings. Use addition operator over `concat()`.
* `slice()`
* `substr()`
* `substring()`
All three accept one or two arguments: where to start and where to stop. For `slice()` and `substring()`, the second argument is the position where capture is stopped. For `substr`, the second argument is the number of characters to return. These methods do not alter the value of the string.
* `slice()` and `substring`: end character not included. Second argument is the position at which the operation stops.
* `substring`: second argument is the number of characters to include.
Omitting the second value assumes the ending position is the length of the string.

###### Negative values as arguments
* `slice()`: a negative argument is the length of the string plus the negative number.
* `substr()`: negative first argument is length plus the negative number. Negative second argument is converted to 0.

##### String Location Methods
* `indexOf()`: starts at beginning of the string.
* `lastIndexOf()`: looks from the end of the string.
Both search the string and return the position of -1 if not found. Both accept optional second argument that indicates the position to start searching.

##### The trim() method

Trims leading and trailing white space in a copy of a string.
* `trimLeft()`
* `trimRight()`

##### String Case Methods
* `toLowerCase()`
* `toLocaleLowerCase()`
* `toUpperCase()`
* `toLocaleUpperCase()`

##### String Pattern-Matching Methods
* `match()`: accepts a single argument which is a regular-expression string or a `RegExp` object.
* `search()`: returns the index of the first pattern match or -1 if not found.
* `replace()`: replaces a given string or regular-expression result.
* `split()`: splits the string at a given string or `RegExp`

##### The localeCompare() Method
Compares two strings. Returns one of three values:
* -1 (or a negative number) if a string comes before the other alphabetically.
* 0 if they are equal.
* 1 (or a positive number) is the string comes after the other alphanbetically.

### Singleton Built-In Objects

#### Global: catchall for properties and objects that don't otherwise have an owning object.
* URI-Encoding Methods: encode URIs so that a browser can accept and understand them.
    *  `encodeURI()`: works on an entire URI. Does not encode special characters.
    * `encodeURIComponent`: works on segment of a URI. Encodes any special character.
    * `decodeURI()`
    * `decodeURIComponent()`
* The eval() Method: Accepts one argument, a string of ECMAScript to execute.  Not hoisted. Use caution when using, particularly when passing user-entered data to it.  Can lead to code injection.
* Global object properties: has several properties, including values and constructors.
* The Window object: The `Global` object's delegate in a browser.

#### The Math Object
* Math Object properties: Several properties related to mathematical calculations. Faster than writing in JS directly.
* The min() and max() methods: Determine smallest or largest in a group of numbers. Used with apply to find min or max in an array.
```
var values = [1, 2, 3, 4, 5, 6, 7, 8];
var max = Math.max.apply(Math, values);
```

* Rounding Methods: Round decimal values to integers.
    * `Math.ceil()`: rounds up
    * `Math.floor()`: rounds down
    * `Math.round()`: standard round function (up for 0.5 or higher).

* The random() Method: Returns a random number between 0 and 1, but not 0 or 1. Can be used to select numbers in a certain integer range:
```
number = Math.floor(Math.random() * total_number_of_choices + first_possible_value);
```
