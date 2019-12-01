# Memoization and Dynamic Programming

From [Web Dev Simplified](https://www.youtube.com/watch?v=WbwP4w6TpCk)

Important topic when it comes to making performant web applications

## Understanding Memoization

### Not Efficient
```
function square(n){
  let result = 0
  for(let i = 1; i <=n; i++){
    for(let j = 1; j <=n; j++){
      result +=1
    }
  }
  return result
}

// takes a while
cosnole.log(square(30000))
// takes the same while
cosnole.log(square(30000))
// takes the same while
cosnole.log(square(30000))
// ...
cosnole.log(square(30000))
```

### Refactor to Efficient

Cache the value base on the inputs

```
const prevValues = []

function square(n){
  if(prevValues[n] != null){
    return prevValues[n]
  }
  let result = 0
  for(let i = 1; i <=n; i++){
    for(let j = 1; j <=n; j++){
      result +=1
    }
  }
  prevValues[n] = result
  return result
}

// First log slow, the rest already computed
cosnole.log(square(30000))
cosnole.log(square(30000))
cosnole.log(square(30000))
cosnole.log(square(30000))
```

## Memoization Use Case: Dynamic Programming

### Fibonacci Sequence

```
function fib(n){
  if(n<=2){
    return 1
  }else{
    return fib(n - 1) + fib(n - 2)
  }
}

console.log(fib(4))
//40 will take quite a while
console.log(fib(40))
//41 will take double time of 40
console.log(fib(40))
```

### Refactor to Efficient
For fb(5) we need to calculate the fibonacci sequence of 4 and 3.

For fb(4) we need fib seq of 3 and 2

that means we calculating fib(3) twice!

```
function fib(n, prevValues = []){
  if(prevValues[n] != null){
    return prevValues[n]
  }
  let result
  if(n<=2){
    return 1
  }else{
    result =  fib(n - 1, prevValues) + fib(n - 2, prevValues)
  }
  prevValues[n] = result
  return result
}

// fib(40) now executes almost instantly
console.log(fib(40))
// fib(100) again almost instantly
console.log(fib(100))
```


## My Use Cases

* HybridHDR
  * Auto Color Saturation: some calculations into complex function remain the same at different inputs
* Auto Check Username
  * SignUp Form: if username tried and exists, no need to send a GET request again to check if username exists