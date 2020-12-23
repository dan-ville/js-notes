[[Functional Programming]]

# Make your own map function
The map method returns an array of the same length as the one it was called on. It also doesn't alter the original array, as long as its callback function doesn't.

In other words, map is a pure function, and its output depends solely on its inputs. Plus, it takes another function as its argument.

```js 

// The global variable
var s = [23, 65, 98, 5];

Array.prototype.myMap = function(callback) {
  var newArray = [];
  // Only change code below this line

  // Only change code above this line
  return newArray;
};

var new_s = s.myMap(function(item) {
  return item * 2;
});
```

Notice that the map method is a function that is available to all Array objects in JS. This means that it must be part of the Array prototype. That's why you can see in the code that we are creating `myMap` by defining it on  `Array.prototype`.

## Solution
The result should be something like this:

```js
// The global variable
var s = [23, 65, 98, 5];

Array.prototype.myMap = function(callback) {
  var newArray = [];
  // Only change code below this line
  for (let i of this) {
    newArray.push(callback(i))
  } 
  // Only change code above this line
  return newArray;
};

var new_s = s.myMap(function(item) {
  return item * 2;
});
```

## Explaining the code:

The pseudo-map function we are creating works basically like this... 

`Array.prototype.myMap = function(callback) {...}`

Here, we define that `myMap` is a function that takes a callback (another function) as its argument.

`var newArray = []` is just initializing an array that will eventually be returned by `myMap`. This is necessary because the original `map` method does not alter the array that it is called on; it returns a new one. That's what we are simulating here.

The actual functionality of `myMap` is found in the next line:
```js
for (let i of this) {
	newArray.push(callback(i));
}

return newArray
```

So, the original `map` method iterates over every item in the array that it is called on and it returns a new array with the results of each iteration. Naturally, we need to use an iterator like `for...of`, which I chose because it's the simplest thing in terms of syntax, in my opinion, for the job here. You can use a regular `for` loop or a `forEach` too.

The keyword `this` is super important here; `this` in this case will refer to the Array that `myMap` is being called on. Without it, what would you put inside the `for...of` loop syntax? `this` acts like a stand-in for the array itself, so that you can access the elements of the array inside the function that is being called on the array. Crazy, right?

Then, we need to call the callback function on every element (in this case, the `for...of` syntax uses *i* to represent each element) and then `push()` that element onto  `newArray`.   

Finally, we return `newArray`.
