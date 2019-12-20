# Create an object from another object in ES6

# One line solution

It uses an arrow function, a self invoked function and the joy of desctructuring assignment.

```
let person = {
  name: "John",
  surname: "Doe",
  age: 24,
  job: "developer"
}

let john = (({age, job}) => ({age, job}))(person)


/* Check out the result in your console:
John:
  {
    "age": 24,
    "job": "developer"
  }
*/
```

Source: [Medium](https://medium.com/data-scraper-tips-tricks/create-an-object-from-another-in-one-line-es6-96125ec6c834)