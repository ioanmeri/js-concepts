# Promises

From [Web Dev Simplified](https://www.youtube.com/watch?v=DHvZLI7Db8E&list=PLZlA0Gpn_vH-0FlQnruw2rd1HuiYJHHkm&index=1)

A Promise in JS is like a promise in real life, where you commit to something like I promise to do something, and that has two results. The Promise is completed (resolved) or failed (rejected).

## Syntax

Anything inside .then is going to run for resolve.

```
let p = new Promise((resolve, reject) => {
  let a = 1 + 1
  if(a == 2){
    resolve('Success')
  }else {
    reject('Failed')
  }
})

p.then((message) => {
  console.log('This is in the then ' + message)
}).catch((message) => {
  console.log('This is in the catch ' + message)
})
```

**.then** is going to be **called when** our **Promise resolves** successfully.

**.catch** is going to be called, if our **Promise is rejected or fails**

Promises are really great when you need to do something that's gonna take a long time in the background (such as downloading an image from a server).

## Callbacks to Promises

```
const userLeft = false
const userWatchingCatMeme = false

function watchTutorialCallback(callback, errorCallback){
  if(userLeft){
    errorCallback({
      name: 'User Left',
      message: ':('
    })
  } else if (userWatchingCatMeme) {
    errorCallback({
      name: 'User Watching Cat Meme',
      message: 'WebDevSimplified < Cat'
    })
  } else {
    callback('Thumps up and Subscribe')
  }
} 

watchTutorialCallback((message) => {
  console.log('Success: ' + message)
}, (error) => {
  console.log(error.name + ' ' + error.message)
})
```

Implement this using Promises instead of callbacks, because this is what Promises were really meant to solve.

No longer callbacks

```
const userLeft = false
const userWatchingCatMeme = false

function watchTutorialPromise(){
  return new Promise((resolve, reject)) => {
    if(userLeft){
      reject({
        name: 'User Left',
        message: ':('
      })
    } else if (userWatchingCatMeme) {
      reject({
        name: 'User Watching Cat Meme',
        message: 'WebDevSimplified < Cat'
      })
    } else {
      resolve('Thumps up and Subscribe')
    }
  }
} 

watchTutorialPromise().then((message) => {
  console.log('Success: ' + message)
}).catch((error) => {
  console.log(error.name + ' ' + error.message)
})
```

With Promises the code is a lot cleaner to write than with using callbacks. Because when you start nesting callbacks you get the callback hell (= code gets intended further and further)!


## Promise All

```
const recordVideoOne = new Promise((resolve, reject) => {
  resolve('Video 1 Recorded')
})

const recordVideoTwo = new Promise((resolve, reject) => {
  resolve('Video 2 Recorded')
})

const recordVideoThree = new Promise((resolve, reject) => {
  resolve('Video 3 Recorded')
})
```

Run all of this in parallel! so we don't have to worry about waiting for one before we start the next.
Send in an array of all the Promises we want to run.

Promise.all is going to run every single of these Promises and as soon as it's done is then going to call .then and .catch methods, depending on if they resolve or fail

```
Promise.all([
  recordVideoOne,
  recordVideoTwo,
  recordVideoThree,
]).then((messages) => {
  console.log(messages)
})
```

## Promise Race

It is just like Promise.all except it will return as soon as the first one is completed, instead of waiting for everything to complete.

```
Promise.race([
  recordVideoOne,
  recordVideoTwo,
  recordVideoThree,
]).then((message) => {
  console.log(message) // Video 1 Recorded (only first message)
})
```
