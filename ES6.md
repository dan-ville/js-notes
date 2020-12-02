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

For example, if you 
### Spread in Function Calls
### Spread with Array Literals
### Spread with Objects

## Rest Params
## Destructuring