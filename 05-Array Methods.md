# Array Methods

From [Web Dev Simplified](https://www.youtube.com/watch?v=R8rmfD9Y5-c)

```
const items = [
  { name: 'Bike',     price: 100  },
  { name: 'TV',       price: 200    },
  { name: 'Album',    price: 10  },
  { name: 'Book',     price: 5    },
  { name: 'Phone',    price: 500 },
  { name: 'Computer', price: 1000 },
  { name: 'Keyboard', price: 25 },
]
```

## filter 

Get all **items** from the list that are **less or equal to 100**.

```
const filteredItems = items.filter((item) => {
  return item <= 100
})

console.log(filteredItems) // (4) [{...}, {...}, {...}, {...}]
```

The great thing about filter and all the other methods for arrays, is that they actually don't change the underline object that you are filtering.


## map

Allows you to take **one array and convert it into a new array**, so all the elements in the array are going to look **slightly different**.

```
const itemNames = items.map((item) => {
  return item.name
})

console.log(itemNames) // (7) ["Bike", "TV", ..., "Keyboard"]
```

## find

Allows you to **find a single object** in an array

Return the item for **the first one where it's true ** (the statement in return )

```
const foundItem = items.find((item) => {
  return item.name === 'Album'
})

console.log(foundItem) // {name: "Album", price: 10}
```

## forEach

Does not return anything! Similar to for loop

```
items.forEach((item) => {
  console.log(item.name)
})
```

## some

Different from the others. **Returns true or false**

```
const hasInexpensiveItems = items.some((item) => {
  return item.price <= 100
})

console.log(hasInexpensiveItems);
```

**If anything below 100**, then this array has inexpensive items in it.


## every 

Checks to make sure that **every single items** fulfills the statement

```
const hasInexpensiveItems = items.every((item) => {
  return item.price <= 100
})

console.log(hasInexpensiveItems) // false
```

## reduce

Different from the others. It's doing some operation on the array and returning a combination of all those different operations.

Get total price:

Runs a function on every single item inside the array. The first method of that function, is going to be whatever the previous iteration of this array returned. The second item is the actual item in the array.

The first time this reducer runs:
  * return currentTotal = 100 + 0 (startingCurrentTotal)

The second time:
  * return currentTotal = item.price + 100 (previousCurrentTotal)

...

```
const total = items.reduce((currentTotal, item) => {
  return item.price + currentTotal
}, 0)
```

currentTotal: the total after each iteration of the array.
second Parameter: the starting point (here start at 0)

Useful when you need to do some kind of **operation cumulatively** 


## includes

It takes a single element

const items = [1, 2, 3, 4, 5]

const includesTwo = items.includes(2)

console.log(includesTwo) // true

When you just need to check if an array has a value, without doing a complex find, especially in simple arrays.
