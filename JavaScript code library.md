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

## Simple multi-dimensional array

```javascript
  var dinnerChoices = [
                        ["Salad", "Soup", "Cheese Plate"], // <-- row 0
                        ["Chicken", "Salmon", "Lasagna"]   // <-- row 1
                      ]

  let firstAppetizer = dinnerChoices[0][0]
  let secondAppetizer = dinnerChoices[0][1]
  let thirdMainDish = dinnerChoices[1][2]

  console.log(firstAppetizer, secondAppetizer, thirdMainDish)

  dinnerChoices[1][0] = "Steak"

  console.log(dinnerChoices[1][0])
```

## Jagged arrays

This example is in C# but the concept is the same. Instead of having a fixed size, multi-dimensional
array, jagged arrays can save space each column only being as large as it needs to be:

```C#
using System;

class Program
{
    static void Main() {
        
        // create jagged array with 3 rows, and as many columns as needed
        int[][] jagged = new int[3][];
        
        // Set row 0
        jagged[0] = new int[2];
        jagged[0][0] = 8;
        jagged[0][1] = 10;
        
        // Set row 1
        jagged[1] = new int[4] {20, 30, 40, 50};
        
        // Set row 2
        jagged[2] = new int[9];
        
        Console.WriteLine("At row 1, col 0: " + jagged[1][0]);
    }
}
```