# Why is Array / Object Destructuring So Useful

From [Web Dev Simplified](https://www.youtube.com/watch?v=NIq3qLaHCIs)

Take an object/array and convert it to smaller elements/variables


## Arrays
```
const alphabet = ['A', 'B', 'C', 'D', 'E', 'F']
const numbers = ['1', '2', '3', '4', '5', '6']
```

Extract the 3 first letters Based on **position**:

```
const [a, b, c] = alphabet
```

What if we want to skip 'B' ?
```
const [a,, c] = alphabet
```

What if we want to get the rest of the elements?

### Spread Operator

```
[a,,c, ...rest] = alphabet

console.log(rest) // ["D", "E", "F"]
```

### Combine 2 arrays

const newArray = [...alphabet, ...numbers]

but for arrays is the same with:

const newArray = alphabet.concat(numbers)

```
console.log(newArray) // ["A", "B", "C", "D", "E", "F", "1", "2", "3", "4", "5", "6"]
```

### Dealing With Functions

```
function sumAndMultiply(a, b){
  return [a+b, a*b]
}

const array = sumAndMultiply(2, 3)

console.log(array) //[5,6]
```

But with Destructuring:

```
const [sum, multiply] = sumAndMultiply(2, 3)

console.log(sum)
console.log(multiply)
```

### Default Values With Destructuring

```
const [sum, multiply, division = 'No division'] = sumAndMultiply(2, 3)

console.log(division) // No division
```

## Objects

```
const personOne = {
  name: 'Kyle',
  age: 24,
  address: {
    city: 'Somewhere',
    state: 'One of them'
  }
}

const personTwo = {
  name: 'Sally',
  age: 32,
  address: {
    city: 'Somewhere else',
    state: 'Another one of them'
  }
}
```

### Destructring an Object

Based on the **name of the key**

```
const { name, age } = personTwo

console.log(name)
console.log(age)
```

### Change Variables

Map name to firstName

```
const { firstName, age } = personTwo

console.log(firstName)
```

### Default Values

```
const { name: firstName = 'john', age, favoriteFood = 'Rice' } = personTwo

console.log(favoriteFood) // Rice
```

### Spread Operator

```
const { name: firstName, ...rest } = personTwo

console.log(rest)
```

**rest** will be an object, but it will not contain name because it was extracted to firstName

```
{
  age: 32,
  favoriteFood: "Watermelon",
  address: {...}
}
```

### Destructuring nested objects

Get the street: Destructure new object

```
const { name: firstName, address: { city } } = personTwo

console.log(city)
```

### Combine Objects

```
const personOne = {
  name: 'Kyle',
  age: 24,
  address: {
    city: 'Somewhere',
    state: 'One of them'
  }
}

const personTwo = {
  age: 32,
  favoriteFood: 'Watermelon',
}
```
Everything in personTwo **will override** everything in personOne

All of the **rest** of **personOne**, and all of the **rest** of **personTwo**

Take everything inside personOne and put in object, and then take of personTwo and also put it
in the same object, but override anything that was already in personOne

```
const personThree = {...personOne, ...personTwo}

console.log(personThree) //age: 32 => overwritten
```

### Use Destructuring inside function arguments

```
function printUser(user){
  console.log(user)
}

printUser(personOne)
```

But what if we only really want to print the name and age?

Most useful part of destructuring!

```
function printUser({ name, age, favoriteFood = 'Watermelon' }){
  console.log(`Name is: ${name}. Age is ${age}. Food is ${favoriteFood}`)
}

printUser(personOne)
```




