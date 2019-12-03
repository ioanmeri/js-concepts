# Closures

From [Web Dev Simplified](https://www.youtube.com/watch?v=3a0I8ICR1Vg)

In other languages, you cannot access variables outside of a function, inside of that function. 
But it is possible in JS, this is what we call a closure.

A global variable is available inside this function:
```
const myName = 'Kyle'

function printName(){
  console.log(myName)
}

printName() // Kyle
```

The entrire JS file is one scope. The function is another scope.

> Every scope has access to everything outside of it's scope. 

The function has access to everything inside outer file!
```
const myName = 'Kyle'

function printName(){
  console.log(myName) // Kyle
}

myName = 'Joey'
printName() // Joey
myName = 'Kate' 
printName() // Kate
```

## Functions inside other Functions

```
function outerFunction(outerVariable){
  return function innerFunction(innerVariable){
    console.log('Outer Variable: ' + outerVariable)
    console.log('Inner Variable: ' + innerVariable)
  }
}

const newFunction = outerFunction('outside') 
newFunction('inside') 
```

How is the **innerFunction** able to **access** the **outerVariable**, **even after is done executing** ?

Because the outerVariable has gone out of scope. That is where closures come in.

What happens is that **innerFunction keeps track of the outerVariable at all times**. Even if the function that defines this variable, is no longer executing anymore (when function exits).

## Common Use Case

When Using **Fetch**, we actually use a Closure. A function defined inside of another function.
The inner function, has access to all of the scope of the outerFunction.

```
function outerFunction(url){
  fetch(url).then(() => {
    console.log(url)
  })
} 
```

**Inner function** has access to the **url variable**, even though fetch is gonna call the .then function **long after outerFunction is being called**.

## Wrap Up
When you have a function defined inside of another function, that inner function has access to variables and scope of the outer function, even if the outer function finishes executing and these variables are no longer available outside of that function.
