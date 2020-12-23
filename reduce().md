`Array.prototype.reduce()`, or simply `reduce()`, is the most general of all array operations in JavaScript. You can solve almost any array processing problem using the `reduce` method.

The `reduce` method allows for more general forms of array processing, and it's possible to show that both `filter` and `map` can be derived as special applications of `reduce`. The `reduce` method iterates over each item in an array and returns a single value (i.e. string, number, object, array). This is achieved via a callback function that is called on each iteration.

The callback function accepts four arguments. The first argument is known as the accumulator, which gets assigned the return value of the callback function from the previous iteration, the second is the current element being processed, the third is the index of that element and the fourth is the array upon which `reduce` is called.

In addition to the callback function, `reduce` has an additional parameter which takes an initial value for the accumulator. If this second parameter is not used, then the first iteration is skipped and the second iteration gets passed the first element of the array as the accumulator.

Review:
1. the `reduce` method iterates through an array and returns a single value by using a callback function
2. the callback function takes 4 arguments; the accumulator, the current element being processed, the index of the current element, and the array upon which `reduce` is called.
	- the accumulator - gets assigned the return value of the callback function from the previous iteration
	
Let's look at `reduce` in depth. If we wanted to use `reduce` to sum up all the values in an array, it would be able to do that; but let's do it without `reduce` for now.

1A
```js
const values = [1, 2, 3, 8, 10, 23, 59];

let sum = 0;
for (let i=0; i < values.length; i++) {
	sum += values[i];
}

console.log(sum);
```

You can also use a `for...of` loop or the `forEach` method, but the regular one demonstrates the control of the index, which is useful for us right now.

For the sake of understanding `reduce`, we will say from now on that `reduce` takes two arguments:  *the accumulator* (which will be the callback function we mentioned earlier) and the *current value.* 

Now, in the code above, we have a for loop that sums all the values of the *values* array and stores the sum in the *sum* variable. Basically, it's *accumulating* the values. 

Hold that thought.

Here's a sum function that reduce can use as a callback, and then pass it into reduce.

1B
```js
function sum(acc, val) {
	return acc + val;
}

let answer = values.reduce(sum);
```

Now you get the sum.  

"But we didn't provide reduce with an initial value?" 

Yes; remember: If this second parameter is not used, then the first iteration is skipped and the second iteration gets passed the first element of the array as the accumulator.

Now, we can take a look at code 1A again and change up the words:
1C
```js
// original
const values = [1, 2, 3, 8, 10, 23, 59];

let sum = 0;
for (let i=0; i < values.length; i++) {
	sum += values[i];
}

console.log(sum);

// new
const values = [1, 2, 3, 8, 10, 23, 59];

let acc = 0;
for (let i=0; i < values.length; i++) {
	acc += values[i];
}

console.log(sum);
```

Now we see what's really going on when we pass the *sum* function to reduce. The accumulator in reduce starts at 0; so, our code initializes a variable *acc* with the value 0. The callback function *sum* that gets passed `reduce` loops through the *values* array and performs `acc += values[i]` at each iteration; so, we added a for loop that does the same thing. 

It's a lot simpler when you compare the functionality side by side.

And if you pass the second argument to reduce and you give it any value other than 0, that's what it's going to start accumulating from! It's the same as if you were to do `let acc = 10;` in code 1C.

Let's refactor our code using ES6 arrow function syntax.

1D
```js
const values = [1, 2, 3, 8, 10, 23, 59];
let answer = values.reduce((acc, val) => acc + val);
console.log(answer);
```

This works as an anonymous arrow function! Instead of having to declare a formal named function elsewhere, we can just create an anonymous arrow function for `reduce` to use as a callback, and we have a nice one-liner.

Let's try another example. How would you use `reduce` to find the maximum value in an array?

The normal way, without `reduce`:

2A
```js
const values = [1, 2, 3, 8, 10, 23, 59];

let acc = 0;
for (let i=0; i < values.length; i++) {
	if (values[i] >= acc) {
		acc = values[i]
	}
}
console.log(acc) // 59
```

Now, let's redo it with a function.
2B 
```js
const values = [1, 2, 3, 8, 10, 23, 59];

function findMax (acc, val) {
	if (val > acc) {
		acc = val;
	}
	return acc
}

let max = values.reduce(findMax);
```

So, findMax is the callback function that reduce is working off. Now, let's refactor for a third time using the anonymous arrow function syntax.

2C 
```js
const values = [1, 2, 3, 8, 10, 23, 59];

let max = values.reduce((acc, val) => {
	if (val > acc) {
		acc = val;
	}
	return acc
})

console.log(max);
```

Now, that may not look like it's considerably more concise, but it's a much more common style when it comes to functional programming, for a number of reasons. One reason is that you don't waste time creating a separate function; you can simply write the callback right in the `reduce` call itself, thereby reducing the number of formal functions you have to work with in the codebase. Also, the ES6 syntax is typically just shorter. 

There's a further way to refactor the code to make it legimately condense, using a [*ternary operator*](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Conditional_Operator). This one is arguably a bit overkill, because it definitely makes things shorter but it also looks like much more esoteric code.

Using a ternary operator looks like this (with *a* representing the accumulator and *b* representing the current value):
2D
```js
const values = [1, 2, 3, 8, 10, 23, 59];

let max = values.reduce((a, b) => b > a ? b : a)

console.log(max);
```

The reason we can use this is because at the heart of the algorithm, all we are trying to do is evaluate if one number is bigger than another (*is a > b?, if so, set a = b, then repeat for the next element in the array*). 

The ternary, or conditional, operator works like this; you have three operands:
1. a condition followed by a question mark (`?`), then
2. an expression to execute if the condition is [truthy](https://developer.mozilla.org/en-US/docs/Glossary/truthy) followed by a colon (`:`), and finally 
3. the expression to execute if the condition is [falsy](https://developer.mozilla.org/en-US/docs/Glossary/falsy).