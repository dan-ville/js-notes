# Classes

Classes are part of [[ES6]], and they are an alternative way of creating Objects. They are syntactic sugar which lets you use a class in place of both a constructor and prototype. 

When you create a class, you use the `class` keyword and you define the constructor within the class. You can define the object properties inside the constructor and the object methods as the other properties.

For examle, here is a class called `Human`.

```js
class Human {
	// instance properties
	constructor (_name, _age, _height, _weight) {
		this.name = _name;
		this.age = _age;
		this.height = _height;
		this.weight = _weight;
	}
	// instance methods
	sayName () {
		console.log(`My name is ${this.name}.`);
	}
}

const human1 = new Human('Danny', 23, 170, 215)
```