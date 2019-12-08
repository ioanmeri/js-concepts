# Modules

From [Web Dev Simplified](https://www.youtube.com/watch?v=cRHQNNcYf6s&list=PLZlA0Gpn_vH-0FlQnruw2rd1HuiYJHHkm&index=4)

Keep your code clean and maintainable!

The main idea behind modules is allowing you to import and export different sections of code, from different files into other files. 

Break apart your code into smaller files, which are easier to understand and reason with later on.

## Example

We want to export the different information about the user, so that we can use it inside our **main.js**, which is being imported inside of our index.html

project/**main.js**

project/**user.js**
```
class User {
  constructor(name, age){
    this.name = name
    this.age = age
  }
}

function printName(user){
  console.log(`User's name is ${user.age}`)
}

function printAge(user){
  console.log(`User is ${user.age} years old`)
}
```

## Types of exports

We can **default export** only **1 thing** (usually the class if there is one)

Export User class as default and functions as standard 

### 1st way:

```
class User {
  constructor(name, age){
    this.name = name
    this.age = age
  }
}

function printName(user){
  console.log(`User's name is ${user.age}`)
}

function printAge(user){
  console.log(`User is ${user.age} years old`)
}

export default User
export { printName, printAge }
```

### 2nd way

```
export default class User {
  constructor(name, age){
    this.name = name
    this.age = age
  }
}

export function printName(user){
  console.log(`User's name is ${user.name}`)
}

export function printAge(user){
  console.log(`User is ${user.age} years old`)
}
```

## Import at main.js

Make sure you put a **./** in front of the module to import it from a relative path,  or **/** for an absolute path.

project/**main.js**
```
import User from '/user.js'

const user = new User('Bob', 11)
console.log(user)
```

This is not enough, will through a SyntaxError. We need to tell index.html that we are using modules

project/**index.html**:

```
<head>
  <script type="module" defer src="main.js"></script>
</head>
```

Import allows you to change the name of the import object: you can use import U instead of import User.

### Import un-default things

Also, you can change the name of the named import using **as**

```
import U, { printName as printUserName, printAge } from '/user.js'

const user = new U('Bob', 11)
console.log(user)
printUserName(user)
printAge(user)
```

## Browser Support

Not many modern browsers support import though, so what most people do is that they use tools such as **babel** to convert their import and export statements & other modern JS features into older JS, so that they can be used in browsers that don't support es6.

Older browsers will completely ignore the script tag because they don't recognize the type="module" part. So it won't even render.

You can use the nomodule attribute, which is recognized by older browsers and ignored by those who support es6.
```
<script nomodule  src="oldmain.js">
```

But use babel anyway. It will automatically do the conversions for you and you don't have to rewrite your code twice.