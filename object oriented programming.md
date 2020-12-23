[[Index]]

# A Tutorial on Objects in JavaScript

## What is an object?

Programming relies on logic and information. All programming languages will offer ways to store, access, and manipulate information using the language syntax and functionality. 

In JavaScript, pretty much everything is an Object. 

We will start by looking at the Object Literal.

## Object Literals  

Objects in JavaScript are used to model real-world objects, giving them properties and behavior just like their real-world counterparts.

A ***property*** of an object is essentially a key-value pair; the *key* is the name or identifier of the property, while the *value* is anything that is stored in the key. 

Here's an example of a "human" object.

```js
let human = {
	name: 'Danny',
	hairColor: 'brown'
}
```

A key can be a single word, but if it is more than one word, it must be wrapped in quotations. The values can be anything--any type of data, from primitives like strings, integers, and booleans, to data structures like arrays and even other objects.

You can access the data in an object using dot or bracket notation. Let's say you want to retrieve the name from the `human` object. 

```js
const name = human.name;
console.log(name) //Danny
```

You can also use bracket notation, but it's more common to use dot notation. However, bracket notation has certain use cases. A property whose key is two words (separated by a space) *must* be accessed using bracket notation. Additionally, bracket notation can be used to perform evaluations. More on that later.

## Methods
Objects can have a special type of property, called a method.

Methods are properties that are functions. This adds different behavior to an object. Here's an example with the human object.

```js
let human = {
	name: 'Danny',
	hairColor: 'brown',
	sayName: function() {
		return 'My name is ' + human.name ".";
	}
}

human.sayName() //"My name is Danny."
```

Notice that we can call the function `sayName` on the `human` object just like we could call any other method like `push()` on an array or `split()` on a string. In reality, all methods are just functions inside object prototypes, which we will read about later.

## This
`This` is a notorious concept in programming. 

Let's try to simplify it.

When you have an object, it can be as large as you want. It may have a thousand properties. If the a certain property needs to refer to the value of another property, it can do so by using the dot notation on the name of the object. However, the `this` keyword can replace the name of the object. Here's a simple example.

```js
let human = {
	name: 'Danny',
	hairColor: 'brown',
	sayName: function() {
		return 'My name is ' + human.name ".";
	}
}

human.sayName()
```

What if the name of the object changed from `'human'` to `'danny'`? You would have to change the function call at the bottom to `danny.sayName()` and do the same in the  `sayName` function definition in the object. This is simple for a short script, but what if it was a very long script? It would help avoid errors to use `this.name`.

But that's just the basics of `this`.

The `this` keyword references the object in the scope it is used in. That's still a vague concept, but hopefully this will clear things up:

An object can be created in a global scope or in a local scope. Since pretty much everything in javascript (arrays, strings, object literals) is an object, `this` can simplify our lives when we need to reference the right object in the right context. This stuff will come together later, I promise.

## Constructor Functions
A constructor function is a function that is used to create new objects. 

Constructors are functions that create new objects. They define properties and behaviors that will belong to the new object. Think of them as a blueprint for the creation of new objects.

Here is an example of a constructor:

```js
function Human() {
	this.name = "Danny";
	this.hairColor = "brown":
}
```

See how we are now using `this` to refer to the object that the constructor function is created. In plain english, `this.name` will mean that *this* object will have a property with a key of *name* and a value of *"Danny"*.

Notice how constructor functions are different from a standard object definition. You want to capitalize the name (by convention, this helps differentiate a constructor and a regular function), and you use semicolons in each new property rather than commas.

That serves as a basic example of a constructor that will allow you to create new Human objects named "Danny" with brown hair. But we may not want to always have the same Human. We might want a "Scarlet" with red hair or a "Daphne" with blonde hair. 

Constructor functions allow this by letting you pass in parameters.

```js
function Human(name, hairColor) {
	this.name = name;
	this.hairColor = hairColor;
}
```

This is a lot more flexible!

So how do we use a constructor function like this? In our code, we can use the constructor at any time by storing it in a variable.

```js
let danny = new Human('Danny', 'brown');
let scarlet = new Human('Scarlet', 'red');
```

It is important to note that constructor functions do not return a value like other functions do! They only define behavior and properties.


## instanceOf
the `instanceof` operator allows you to compare an object to a constructor function. If the object was created using the constructor function, it will return true. If not, it returns false.

```js
let danny = new Human('Danny', 'brown');
danny instanceof Human; // => true
```

## Own Properties, Prototypes, and Prototype Properties

### Own Properties
Whenever you create an object using a constructor, you create an *instance* of that object. Every instance of the object will have properties, and the properties are called *own properties*. This is different to *prototype properties*, which we will see later.

The main thing to understand about own properties is that they are defined directly on each *instance* of an object. 

So far, we've used the constructor function to create unique instances of the Human object, where the properties always had different values. What if we wanted to create a property that was the same for all instances? For example, every Human has two legs. We could give the object a number of legs property set to two.

```js
function Human(name, hairColor) {
	this.name = name;
	this.hairColor = hairColor;
	this.numLegs = 2;
}
```

Now, every instance of Human will have a property `numLegs` with a value of 2.

However, since every `numLegs` property will be set to 2, you will essentially have a duplicated variable inside each `Human` instance.

If there were a thousand instances, that would be a lot of duplicates. The better way to do this is to create a ***prototype***.

### Prototypes and Prototype Properties
```js
Human.prototype.numLegs = 2;
```

This is going to add a `prototype` *property* to the `Human` constructor. Do you see that the dot notation is: `numLegs` on `prototype` on `Human`? The fact that `numLegs` is accessed through dot notation means... that the `prototype` property is actually an object! Maybe things are starting to come full circle now.

But that won't last long xD

So, since `prototype` is an object (within an object), and therefore you don't have to define prototype properties on separate lines. You can just code out the entire object at once, like this:

```js
Human.prototype = {
	numLegs : 2,
	eat: function() {
		console.log("nom nom nom")
	}
}
```

Notice that this just looks like a regular object syntax, unlike the constructor syntax.

With this, every instance of `Human` will have the `numLegs` and `eat` properties. These have been created using the prototype, instead of being created directly in the constructor function, like *own* properties are.

### The Constructor Prototype

Now, just like `prototype` is a property on an object, `constructor` is also a property.  The constructor property is a reference to the constructor function that created the instance. It's a special property that lets you check what kind of object something is. You can use it to return true or false, like this:

```js
if (danny.constructor === Human) {
		return true
	} 
	else {
		return false
	}
```

However, the constructor property can be overwritten, so it's generally better to use `instanceof` to check the type of an object.

### Remember to Set the Constructor Property when Changing the Prototype

Now, it's important to note:
**If you manually create a prototype by setting it to a new object, there is a big issue--it erases the `constructor` property**

The easy fix is just to set the constructor property yourself in the prototype object definition:
```js
Human.prototype = {
	constructor: Human,
	numLegs : 2,
	eat: function() {
		console.log("nom nom nom")
	}
}
```

### Understand Where an Object’s Prototype Comes From

Just like people inherit genes from their parents, an object inherits its prototype directly from the constructor function that created it. 

In other words, if you create an object after having defined the constructor function for that object, the prototype for that object will be inherited from the constructor. This establishes the relationship between constructors and prototypes. You can check the relatonship with the `isPrototypeOf` method:

```js
function Human(name) {
	this.name = name;
};

Human.prototype = {
	constructor: Human,
	numLegs : 2,
	eat: function() {
		console.log("nom nom nom")
	}
};


let danny = new Human("Danny");

Human.prototype.isPrototypeOf(danny) // returns true
```

### Understand the Prototype Chain

All objects in JavaScript (with a few exceptions) have a `prototype`. Also, an object’s `prototype` itself is an object .Because a `prototype` is an object, a `prototype` can have its own `prototype`!

There is actually an object that comes built into JavaScript called... *Object.* Yet, it's very straightforward. But, this is important, because you will be able to see that any prototype for an object that you create can be a prototype of the Object prototype; that is, since your object's prototype is itself an object, it has its own prototype property that comes from the `Object` prototype. Sorry. That can be confusing.

Anyway, we can check it like this:
```js
Object.prototype.isPrototypeOf(Human.prototype);
```

In plain English, that says: "does the Human prototype object have its own prototype property that comes from the Object prototype?"

Let's clear things up by establishing that Object is a *supertype*. It is a supertype for *all* objects in JavaScript. Human is a *supertype*, but only for objects created with the Human constructor. Therefore, 'danny' and 'scarlet' are *subtypes*.

### Inheritance 

When you are writing code, the principle of DRY (Don't Repeat Yourself) is very important. You can use supertypes and inheritance in objects to avoid creating multiple prototypes that have the same functionality. 

You might have a pair of prototypes that share a function, such as:
```js
Dog.prototype = {
	constructor: Dog,
	describe: function() {
		console.log(`My name is ${this.name}`);
	}
}


Cat.prototype = {
	constructor: Cat,
	describe: function() {
		console.log(`My name is ${this.name}`);
	}
}
```

This method is not DRY because the `describe()` method is found in two places. Instead, it would be better to create a `supertype` (or parent). Let's call it Animal.

```js
function Animal() {}; // an empty constructor, just for the prototype to make sense

Animal.prototype = {
	constructor: Animal,
	describe: function() {
		console.log(`My name is ${this.name}`);
	},
	eat: function() {
		console.log(`nom nom nom`)
	}
}
```

Now we would be able to remove the `describe()` function from Cat and Dog.

But now we need to establish the inheritance for Cat and Dog, so that they will be connected to the Animal prototype and use its methods without having to define them again.

For now, we will use an alternative syntax to creating instances of objects.
```js
// previous syntax
let animal = new Animal();
// new syntax
let animal = Object.create(Animal.prototype);
```

`Object.create(obj)` simply reates a new object and sets the passed in *obj* as the object's prototype. 

```js
let animal = Object.create(Animal.prototype);
```

Here, `animal` is created with the `Animal.prototype` as its prototype.

The next step is to set the prototype of the subtype (or child) to be an *instance*  of the supertype (or parent). 

Remember that here the `Animal` object is the supertype and `Cat` and `Dog` are the subtypes.

The way we go about setting the prototype of the subtypes is:

```js
Dog.prototype = Object.create(Animal.prototype);
Cat.prototype = Object.create(Animal.prototype);
```

To review inheritance:
1. The first step is to make a constructor function for the parent/supertype and then create its prototype
2. The next step is to set the prototype of the child/subtype to be an *instance* of the supertype. Remember that we are doing this with the `Object.create()` method.

### Reset an Inherited Constructor Property

Whenever you establish inheritance for an object by making it inherit from another object, a supertype, the inheritance will also include the supertype's constructor property.

```js
function Bird() {};
Bird.prototype = Object.create(Animal.prototype);
let duck = new Bird();
duck.constructor // function Animal(){...}
```

Thus, we need to reset the constructor property of the subtype or it will show that it was created using the supertype's constructor.

```js
Bird.prototype.constructor = Bird;
duck.constructor // function Bird(){...} 
```

We demonstrate this here on a single line, but usually you should do this in the protoype object of each subtype.


## Use Closure to Protect Properties Within an Object from Being Modified Externally
When you create an object *outside* of a constructor function (aka, just using a standard object definition), the variables inside that object are considered **public**. Public variables can be accessed and modified by *any* part of your code, as they are in the global scope. 

However, there is plenty of information that you might want to keep private, such as a password or a bank pin. 

To make a variable *private*, the easiest thing to do is to create that variable *inside* a constructor function. This changes the scope of that variable to be within the constructor function as opposed to being globally available.

Then, you can create a method your constructor that *returns* the private variable, so that later if you want to access that variable somewhere else in your code, all you need to do is call the method. These kinds of methods are called **priveleged** methods, because they have priveleged access to private information.

Here's an example
```js
function Bank () {
    let password = 1234; // private variable

    // publicly available method that a Bank object can use
    this.getPassword = function () {
        return password;
    }
}

let bankAccount = new Bank();
bankAccount.getPassword() // returns 1234
```

## Immediately Invoked Function Expressions
A common pattern in JavaScript is to create a function that gets called immediately (as opposed to writing a function declaration on one line and then writing a function call on another line).

Here's what a normal function declaration and invocation looks:
```js
function lol() {
    console.log("Supercalifragilisticexpialidocious");
};

lol(); //returns that whole silly phrase
```

Here's how an immediately invoked function expression is written:
```js
(function(){console.log("Supercalifragilisticexpialidocious")})();
```
Notice that (1) it's an anonymous function, and (2) there are two sets of parenthesis on the outside. One set goes around the whole function declaration, and then there is another set of parentheses which are how the function gets called.

## Use an IIFE to Create a Module
Earlier, we saw how we could create mixins to group together different functions to be given to objects that might otherwise be unrelated. Remember that a mixin is supposed to take in an object as an argument and then assign a function to the passed in object. 

A more advanced concept is to group together mixins *inside* of an immediately invokved function expression that *returns* the actual mixins, and then save that IIFE to a variable. This effectively makes a module out of that variable name, and by making a module, we now have the ability to give the functionality of those mixins to any object we pass to the module! 

Here's how it looks.

```js
// Step 1: create mixins
    function greetMixin(obj) {
        obj.greet = function(){
            console.log("Hello there.");
        }
    }

    function jumpMixin(obj) {
        obj.jump = function() {
            console.log("I am jumping");
        }
    }

// Step 2: Create an IIFE saved to a variable
let actionModule = (function(){
    return {
        //return mixins here
    }
})();

// Step 3: Put the mixins inside the return statement of the IIFE 
let actionModule = (function(){
    return {
        function greetMixin(obj) {
        obj.greet = function(){
            console.log("Hello there.");
        }
        }

        function jumpMixin(obj) {
            obj.jump = function() {
                console.log("I am jumping");
            }
        }
    }
})(); // the two parentheses cause the function to be immediately invoked

// Step 4: Use the module, which has mixins that accept an object to give that object the mixin functionality
actionModule.greetMixin(human);
human.greet()
```