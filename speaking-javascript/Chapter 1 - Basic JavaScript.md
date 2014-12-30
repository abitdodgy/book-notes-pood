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

* JavaScript has no block level scope. Instead, it keeps a function scope, and this can be a major source of pain unless you are familiar with this subtlety. 

  ````javascript
  var funcs = [];
  for (var i = 0; i < 5; i++) {
    funcs.push(function () {
      return i;
    });
  }
  funcs[1]();
  5 // returns 5 instead of 1
  ````
  
  The above code will return 5 instead of 1 because the closure will return the current value of the variable, which will be 5 when the loop terminates, and not the value of the variable at the time of the function creation. To avoid this we can use an IIFE, or an *immediately invoked function expression*.
  
  ````javascript
  var funcs = [];
  for (var i = 0; i < 5; i++) {
    (function () {
      funcs.push(function() {
        return i;
      });
    }());
  }
  funcs[1]();
  1
  ````
  
* Objects in JavaScript are typicall key value pairs. The key is a string, and values any JavaScript value, including methods. Objects have automatic getter and setter methods. 

  ````javascript
  var mohamad = {
    name: "Mohamad",
    description: function () {
      return "This is " + this.name;
    }
  };
  mohamad.description(); // This is Mohamad
  mohamad.description    // a string representation of the function
  mohamad.name()         // Uncaught TypeError: string is not a function
  mohamad.name           // "Mohamad"
  mohamad.age            // undefined
  ````
  
  You can set properties arbitarily too.
  
  ````javascript
  mohamad.age = 33;
  mohamad.age; // 33
  ````

  The `in` operator checks if a property exists.
  
  ````javascript
  'age' in mohamad;     // true
  'height' in mohamad;  // false
  ````

  The `delete` operator deletes a property. If the property does not exist, nothing happens.
  
  ````javascript
  delete mohamad.age;
  ````

  Property keys can be set arbitary strings, or none-identifiers. We must use square brackets.
  
  ````javascript
  var mohamad = { 'my mental age': 33 };
  mohamad['my mental age']; // 33
  mohamad['my mental age'] = 12;
  ````
  Square brackets allow us to compute key names.
  
  ````javascript
  mohamad['my mental ' + 'age']; // 12
  ````
  
  We can extract methods from objects, but they lose their connection to the object.
  
  ````javascript
  var description = mohamad.description;
  description();
  TypeError: Cannot read property 'name' of undefined
  ````
  
  To avoid this we can use `bind()`, which creates a new method that has a value for `this`.
  
  ````javascript
  var description = mohamad.description.bind(mohamad);
  description(); // "This is Mohamad"
  ````
  
* Functions have the `this` keyword, which can be inconvenient when nesting functions, since `this` will change context. The following example will not work because `this.name` will return undefined, since it refers to the function within the loop, and not the outer function.

  ````javascript
  var oscar = {
    name: "Mohamad",
    friends: ["Ali", "Hassan"],
    sayHi: function() {
      this.friends.forEach(function (friend) {
        console.log(this.name + " says hello to " + friend);
      });
    }
  }
  ````

  A common way to fix this is by saving this to a variable before the inner function executes, since inner functions have access to their parent scope.
  
  ````javascript
    sayHi: function() {
      var that = this;
      this.friends.forEach(function (friend) {
        console.log(that.name + " says hello to " + friend);
      });
    }
  ```
  
  Or, in this case, `forEach` accepts a second argument for the value of `this`.

  ````javascript
    sayHi: function() {
      this.friends.forEach(function (friend) {
        console.log(that.name + " says hello to " + friend);
      }, this);
    }
  ```

* Functions in JavaScript can also be constructors for new objects. Creating a new object has two parts. First the construtor sets up instance data, and second the object prototype sets methods. The data of the constructor is specific to each instance, while the object prototype methods are inherited by all instances of the class.

  ````javascript
  var Mohamad(name, age) {
    this.name = name;
    this.age = age;
  };
  
  Mohamad.prototype.greet = function (name) {
    return this.name + " says hello to " + name;
  };
  
  var mohamad = new Mohamad("Mohamad", 33);
  mohamad.greet("Mario");
  ```
  
* If you work with Ruby, JavaScript iteration will be slightly different since JavaScript does not use blocks. But anonymous functions are similar enough.

  ```javascript
  ["apples", "bananas", "oranges"].forEach(function (element, index) {
    console.log(element + " is at index " +  index);
  });
  ```
  
  Another example using `map`.
  
  ```javascript
  ["apple", "banana", "orange"].map(function (element) {
    element + "s"
  });
  ```

* Finally, always use `return`. Those used to working with Ruby will do well to remember using `return`.


  
  
