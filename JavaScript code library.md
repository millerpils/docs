 IIFE# JavaScript

## Relational operators

## == and ===

What's the difference?

== checks the value only
=== checks the value AND the type (strict equal)

```javascript
let example1 = 10;
let example2 = '10';
console.log(example1 === example2) <--- false!
```

## Map

```javascript
  let newArr = oldArr.map((val, index, arr) => {
    // return element to new Array
  });

  let newArr = oldArr.map( function(val, index, arr) {
    // return element to new Array
  });
```

## String interpolation

Avoid doing:

```javascript
console.log(var + ' ' + var);
```

Instead, use:

```javascript
console.log(`${firstName} ${lastName}`);
```

## Trim()

Removes whitespace from a string

```javascript
console.log(`${firstName} ${lastName}            `.trim());
```

## Arrays

### Push 

Add items to the end of the array

```javascript
let example1 = [5, 7, 6];

example1.push(8, 9, 10);

[5, 7, 6, 8, 9, 10]
```

### Pop

Removes the last value:

```javascript
example1.pop();

[5, 7, 6, 8, 9]
```

### Spread operator

Creates a new array based on another

```javascript
let example1 = ['Dylan', 5, true];

let example2 = [...example1];

["Dylan", 5, true]
```

## Objects

## hasOwnProperty

Returns true/false if an object has a certain key

```javascript
let example1 = {
    firstName: 'Dylan',
    lastName: 'Israel',
    address: {
        city: 'Austin',
        state: 'Texas'
    },
    age: 30,
    cats: ['Milo', 'Tito', 'Achieles']
};

example1.hasOwnProperty('firstName2')
= false
```

## Set (es6)

A Set is a data structure that stores unique values of any type. To test uniqueness, we use
the strict equals operator:

```javascript
function testJackpot(result) {
  let set = new Set(result).size === 1
  
  console.log(set)
}

testJackpot(['@', '@', 'i', 'i']) <-- false
testJackpot(['@', '@', '@', '@']) <-- true
```

## IIFE

IIFE (Immediately Invoked Function Expression) is a JavaScript function that runs as soon as it is defined.

```javascript
(function () {
  // herp derp
})
();
```