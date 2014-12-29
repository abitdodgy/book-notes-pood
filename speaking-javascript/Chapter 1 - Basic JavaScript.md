### Chapter 1 - Basic JavaScript

Some useful things to remember from this chapter.

* JavaScript syntax is mostly made up of *expressions* and *statements*. Statements do things and expressions produce values.

  ````javascript
  var statement = "This is a statement";
  3 * 3; // This is an expression
  ````
  An expression can be used in lieu of a statement whenever JavaScript expects a statement. A method call, for example, is a statement that produces a value, which is an expression.

  ````javascript
  multiply(1, 2);
  ````

* All values (booleans, numbers, strings, arrays, etc...) in JavaScript have properties, and each property is made up of a key (name) and a value.
  ````javascript
  var string = "abc";
  string.length
  3
  ````

* JavaScript makes an arbitary destinction between values: They are either primitives, or objects:
  - *primitive values* are boolean, numbers, strings, `null`, and `undefined`
  - all other values are objects

* Strictly speaking objects have a unique identity and are only equal to themselves. Objects are **mutable**, and they are **compared by reference**.

  ````javascript
  var obj1 = {};
  var obj2 = {};
  obj1 === obj2;
  false
  obj1 = obj2;
  obj1 === obj2;
  true
  obj1.name = "Mohamad";
  objt.name;
  "Mohamad"
  ````

* In contrast, primitives encoding the same value are considered equal. Primitives are **compared by value** and they are **immutable**. Reading an unknown property returns `undefined`.

  ````javascript
  var str1 = "abc";
  var str2 = "abc";
  str1 === str2;
  true
  1 === 1;
  true
  str.length;
  3
  str.length = 1;
  str.length;
  3
  ````
* `undefined` means no value. Uninitialised variables, missing parameters, and missing properties are undefined.

  ````javascript
  var hello;
  undefined
  function f(x) { return x; }
  f();
  undefined
  var obj = {};
  obj.name;
  undefined
  ````
* `null` means "no object". That its type returns 'object' is a bug that can't be fixed. It is used as a nonevalue whenever an object is expected. It can be used to assign an object a nonevalue.
 
* `false`, `NaN`, `-0`, `0`, `''`, `undefined`, and `null` evaluate to false. This is why you can use the following handy shortcut without explicitly worrying about the value type.

  ````javascript
  if (!x) {}; // It doesn't matter what x is as long as it's false
  ````
* JavaScript has two operators to categorise values: `typeof`, used for primitive values.

  ````javascript
  typeof true;
  boolean
  typeof {};
  'object'
  ````
  
  `instanceof` used for objects. It returns true if value is an object that has been created by the constructor `Constr`.

  ````javascript
  // value instance Constr
  var mohamad = new Mohamad();
  mohamad instanceof Mohamad();
  true
  [] instanceof Array;
  true
  ````

  Any value can be used whenever JavaScript expects a boolean value. Other than the values considered `false`, described above, everything else is considered `true`. Values can be cooerced into boolean.

  ````javascript
  Boolean(0);
  false
  Boolean("hello");
  true
  ````
* Javascript has strict equality operators `===`, and leniet equality operators `==`. Lenient equality operators consider too many values as equal, and can hide bugs. This is why it is recommended to use strict equality operators.

* All numbers in JavaScript are floats.

  ````javascript
  1 === 1.0;
  true
  ````
  
* `Infinity` is used as an error value. `Infinity` is larger than all numbers except `NaN`, and `-Infinity` is smaller than all numbers except `NaN`. This makes it useful for setting minimum and maximum values.

* Function expressions are functions declared as a variables, or passed as arguments. Function expressions produce a value, and so can be passed as arguments.

  ````javascript
  var greet = function (name) {
    return "Hello, " + name;
  };

  function one(function two(1, 2) {
  });
  ````
  
*  Function declarations are hoisted. This allows you to call functions that are defined later.

  ````javascript
  function one(name) {
    two();
    function two() {
    }
  }
  ````
  
  `var` declarations are also hoisted, but their assignments are not.

  ````javascript
  function one(name) {
    two(); // two is undefined
    var two = function () {
    }
  }
  ````

* You can pass functions any number of arguments and the compiler will not complain. You can use the special keyword `arguments`, which is similar to an array, to inspect arguments passed into a function. To enforce arity you can check the length of `arguments`. You can assign default values using `||`.

  ````javascript
  function greet(name) {
    var name = name || "Mohamad";
    return "Hello, " + name;
  }
  ````
  
* `'use strict';` or strict mode, enables more warnings and forces you to use a cleaner syntax. It can be declared within `script` tags, and even inside a function.


