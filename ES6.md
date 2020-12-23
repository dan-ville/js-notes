[[Index]]

# EcmaScript 2015 (ES6)

## Default Parameters
You can add a default value for a parameter that is included in your function even when there are no arguments passed in. Simply set the parameter equal to some value in the function declaration.

For example, here the parameter `name` will have a default value of 'Danny' if no arguments are passed in.
```js
function nameChild(name='Danny'){
	console.log(`The name of this child is ${name}.`)
}

nameChild('Eddie') // 'The name of this child is Eddie.'
nameChild('Danny') // 'The name of this child is Danny.'
```

## Spread 
Spread syntax allows an iterable to be expanded in places where the syntax would normally call for an argument or element (such as a function call parameter) would be expected, or in an object expression where key-value pairs are expected.

The word "expansion" here means that the items of the iterable will be *spread* into separate arguments and passed into where you designate. 

### Spread in Function Calls
For example, if you wanted to get the max number in a set of numbers, you could do:
```js
Math.max(1, 5, 12, 293, 3) // returns 3
```

But what if you needed to pass an array into `Math.max()`? It expectes separate numbers as arguments.

Well, the `...` (spread) operator can do this. It will take the individual items in an array and spread them into separate arguments inside the method call `Math.max()`. 

It looks just like this:
```js
const nums = [1, 5, 12, 293, 3];
Math.max(...nums); // returns 3
```

It may not look like much now, but it's incredibly useful to be able to do this. 

### Spread with Array Literals
You can spread arrays into other arrays. For example, you could perform *array concatenation* easily with the spread operator.

```js
const dogs = ['beagle', 'terrier', 'boxer'];
const cats = ['tabby', 'ragdoll', 'siamese'];
const pets = [...dogs, ...cats] // 

console.log(pets) // ['beagle', 'terrier', 'boxer', 'tabby', 'ragdoll', 'siamese']
```

It works with other iterables too. You can spread a string into an array like so:
```js
const helloArr = [..."hello"];
console.log(helloArr) // ['h', 'e', 'l', 'l', 'o']
```

### Spread with Objects
And it also works with object literals and other objects!
```js
const dogs = {
	legs: 4;
	family: "Caninae"
};

const cats = {
	legs: 4,
	family: "Felidae"
};

const blackCat = {...cats, color: "Black"};

// There is a conflict when there is a property of the same name. The property that will be applied to the spread that was spread into object comes from the *first* object that was spread. In this case, the 'legs' property has the same value in both objects, but the 'family' property has different values in each.

const catDog = {...cats, ...dogs} // family prop in catDog will be 'Felidae'
```

## Rest Params
Inside of every function, JS automatically creates an *arguments* object. It is an **array-like object**, characterized by having a length property (like arrays) but no array methods available (like `push` and `pop`). The `arguments` object will contain all the arguments passed to the function, and it is NOT available in arrow functions (the only exception)!

The problem is that because the *arguments* object is not an actual array, we can't use things like `reduce()` on it. For example, if we wanted to write a sum function with arguments, theoretically it would look like this:

```js
function sum() {
	return arguments.reduce((total, el) => total + el)
}
```

But this won't work because arguments is not an array!

This is a big shortcoming, so the *rest* parameter solves this for us. It looks exactly like the *spread* operator, but it goes in the function parameters.

```js
function sum(...nums) {
	return nums.reduce((total, el) => total + el)
}
```

This will work because `...nums` collects all the parameters passed to the function into an array for us to use in the function. 

It's called *rest* because it collects the *rest* of the parameters passed in... Which implies that we can pass in some parameters before it.  Simply pass in parameters separated by commas, and then use the *rest* notation to use the rest of the arguments inside the function to use as an array for whatever you want. 

For example:
```js
function announceWinners(first, second, everyoneElse) {
	console.log(`First place: ${first}!`);
	console.log(`Second place: ${second}!`);
	console.log(`Thanks to everyone else: ${everyoneElse}.`);
}

announceWinners("Danny", "Juan", "Pablo", "David", "Santi"); 
// Pablo, David, and Santi will be collected into an array and used in the 3rd console.log statement.
```

## Destructuring
The concept of *destructuring assignments*, or destructuring, is the ability to unpack values from arrays, or properties from objects, into distinct variables.

You can define a variable like this:

```js
const foo = ['one', 'two', 'three'];
```

But also like this:

```js
const [red, yellow, green] = foo;
console.log(red); // "one"
console.log(yellow); // "two"
console.log(green); // "three"
```

In those examples, the variable is declared (initialized) and assigned (given a value to reference) simultaneously.

But the variable declaration and assignment can also happen separately.

```js
let a, b;

[a, b] = [1, 2];
console.log(a); // 1
console.log(b); // 2
```

But a *destructuring assignment* will allow you to destructure, or "extract", a value from an array into a separate variable assignment **without changing the array or reassigning the values in it**. 

```js
const items = [1, "red", "blue", 2, 91];
// this destructuring assignment creates two variables, number and bestColor, and assigns them the 1st and 2nd values of the items array
const [number, bestColor] = items; 

console.log(number) // 1
console.log(bestColor) // "red" 
```

This syntax also provides an easy way of swapping two variable values in one expression:

```js
let a = 1;
let b = 3;
console.log(a) // At this point, a returns 1
console.log(b) // and b returns 3

[a, b] = [b, a]; // the destructuring assignment
console.log(a); // now, a returns 3
console.log(b); // and b returns 1
```

You can even destructuring assignments to parse an array returned from a function and store the values:

```js
function f() {
	return [1, 2];
}

let [a, b] = f(); // destructuring 
console.log(a) // 1
console.log(b) // 2
```

The rest parameter also works:
```js
const [a, b, ...arr] = [1, 2, 3, 4, 5, 7];
console.log(a, b); // 1, 2
console.log(arr); // [3, 4, 5, 7]
```

You also don't have to stick to just destructuring arrays. Destructuring objects is possible too, and it's typically more common. One reason is that with an array, the order of the destructuring assignment matters. Notice that in the previous example the function returned an array with the numbers 1 and 2, in that order, and our destructuring assignment set the values of a and b in that same order. 

But with objects, the order is irrelevant because you will assign things based on the property key.

Let's say you had a Facebook user object.
```js
const user = {
	firstName : "Daniel",
	lastName : "Villegas",
	email : "sillygoose@freemail.com",
	password: "1-800-222-2good4u",
	birthplace: "Medellin, Colombia"
}

//it would be really annoying to write several lines of variable assignments
const firstName = user.firstName;
const lastName = user.lastName;
const email = user.email;
```

So instead, you can use a destructuring assignment.

```js
const user = {
	firstName : "Daniel",
	lastName : "Villegas",
	email : "sillygoose@freemail.com",
	password: "1-800-222-2good4u",
	birthPlace: "Medellin, Colombia"
}

const {email, firstName, lastName, password, birthPlace} = user; // all 5 variables created on one line!
```

Furthermore, in the destructuring assigment, you can give the variables a different name by using a colon.

```js
const {firstName : first} = user;
```

This will create a variable called `first` that uses the value found in user.firstName!

If the property in the object does not exist, the variable will have a value of undefined.  

Additionally, an object can be destructured in to a function argument itself.

```js
const profileUpdate = (profileData) => {
  const { name, age, nationality, location } = profileData;
  // do something with these variables
}
```
That example destructures the profileData object inside the profileUpdate variable.  But the same thing can be done in place.

```js
const profileUpdate = ({name, age, nationality, location}) => {
	// do something with these variables
}
```

Basically, this would still take in an object as an argument in the function parameters, but the destructuring happens immediately. Of course, this assumes that the object being passed in will have each of those property key names.

Let's finish up with some more examples using the `movies` array.

```js
const movies = [
 	{
		title: "Joker",
		score: 95,
		year: 2019
	},
	{
		title: "The Bourne Identity",
		score: 92,
		year: 2002
	},
	{
		title: "Doubt",
		score: 94,
		year: 2008
	},
	{
		title: "Sharknado",
		score: 35,
		year: 2013
	},
	{
		title: "Fantastic Beasts and Where to Find Them",
		score: 74,
		year: 2016
	},
	{
		title: "Troy",
		score: 85,
		year: 2004,
	},
	{
		title: "Ocean's Eleven",
		score: 98,
		year: 2001
	}
]
```

Now, if you haven't watched every one of those movies (except Sharknado), you can't be trusted.

But you can also use destructure this array in different ways.

Let's write a function that uses `filter()` to give us all the movies above a score of 90.

```js
const bestMovies = movies.filter((movie) => movie.score >= 90);
```

That code says "for every item (movie) in the movies array, return the items where you find a score of 90 or above."

We can also write it this way, destructuring `score` immediately:
```js
const bestMovies2 = movies.filter(({score}) => score >= 90);
```

In this example, it's only a little shorter. But it demonstrates the capability of destructuring. It means we don't have to bother with the dot notation. JavaScript already knows that we are working off the `movies` array, and the `filter()` method will loop through each item in the array. Since each item is an object, in each iteration of `filter()` we are extracting the score property from the object that is being passed in.

If we wanted to console.log several statements using destructuring, we might use the `map()` method.

We could do it like this:

```js
const releaseYears = movies.map((movie) => {
		return `${movie.title} was released in ${movie.year}.`
	}
)
```

Or, we could make it simpler.
```js
const releaseYears = movies.map({title, year} => {
		return `${title} was released in ${year}.`
	}
)
```

It's simpler because we don't have to reference `movie` everywhere in the function using the dot notation. Take your pick. I'll go with destructuring.