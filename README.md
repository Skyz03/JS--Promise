# JS--Promise

JavaScript Promises - Explain like I am Five:

[Article Link](https://blog.greenroots.info/javascript-promises-explain-like-i-am-five)

The Jack and Jill story which has grandparents(as consumers). The grandparents are also busy discussing about the daily routine which is they are not waiting for water but are working and will start cooking once the kids are back with water.

There can be two possibilities: 
1. Jack can come down with the water.
2. Jack fell down (disaster) and did not get the water.

In this short story, there is a promise of getting the water using the activity of fetching it. The promise can get fulfilled(getting the water) by the kids or reject due to the disaster. Also, grandparents were not sitting idle and were planning their day.

The JS promises also work in a similar way. We create them to fetch asynchronously(configuration, data store) which means we do not want to wait for the response but we can continue to work on the response when its available. <br>

<table><thead><tr><th>In Real Life with JS</th><th>In Our Story</th></tr></thead><tbody><tr><td>Promise </td><td>Water fetching by Jack and Jill</td></tr><tr><td>Executor Function </td><td>Fetch the Water </td></tr><tr><td>Activity</td><td>Fetch</td></tr><tr><td>Expected data in response </td><td>Water</td></tr><tr><td>Consumer </td><td>Grandparents </td></tr><tr><td>Resolve/fullfilled</td><td>Successfully get the water </td></tr><tr><td>Reject </td><td>Disaster / not get water</td></tr><tr><td>Task after getting the data </td><td>Cooking</td></tr></tbody></table>

## Promise in JS
A promise is a JavaScript object that allows you to make asynchronous(aka async) calls. It produces a value when the async operation completes successfully or produces an error if it doesn't complete.

```
// Example
let promise = new Promise(function(resolve, reject) {    
    // Do something and either resolve or reject
});
```

We need to pass a function to the Promise Constructor. That function is called the executor function(Remember, fetching the water?). The executor function takes two arguments, resolve and reject. These two are callback functions for the executor to announce an outcome.

The resolve method indicates successful completion of the task(fetching water), and the reject method indicates an error(the disaster). You do not implement the resolve/reject method. JavaScript provides it to you. You need to call them from the executor function.

```
// Example of Resolve
let promise = new Promise(function(resolve, reject) {
    // Got the water
    let value = 'water';
    resolve(value); // An assurance of getting the water successfully
});
```

## Promise Object & State

In the Jack and Jill story, the grandparents were not waiting for the kids to fetch the water. They were planning the day in the meantime. 
The promise object should be capable of informing the consumers when the execution has been started, completed (resolved), or returned with error (rejected).

### The promise object has 3 states:
1. Pending 
When the execution function starts. In our story, when Jack and Jill start to fetch the water.

2. Fulfilled
When the promise resolves successfully. Like, Jack and Jill are back with the water.

3. Rejected
When the promise resolves successfully. Like, Jack and Jill are back with the water.


### The promise object has 3 results:
1. Undefined
Initially, when the state value is pending.

2. Value 
When the promise is resolved.

3. Error
When the promise is rejected.

![image](https://user-images.githubusercontent.com/42742924/156974550-360eda98-61d2-4d80-b643-32e9e3191011.png)

## Handling Promises by the Consumer(Grandparents need to be informed so how it handles are by given methods):

A consumer can use it to know the state(pending, fulfilled, or rejected) and the possible outcomes(value or error) from it.
These properties are internal. They are code-inaccessible, but they are inspectable. It means that we will be able to inspect the state and result property values using a debugger tool, but we will not be able to access them directly using the program.

So, there are 3 handlers for the above problem.
1) .then()
2) .catch()
3) .finally()

These methods help us create a link between the executor and the consumer when a promise resolves or rejects.

![image](https://user-images.githubusercontent.com/42742924/156975043-25dc6675-b934-4c56-a970-ff400757ba6f.png)

### .then() Handler
We get a .then() method from every promise. The sole purpose of this method is to let the consumer know about the outcome of a promise. It accepts two functions as arguments, result and error. 

```
// Both
promise.then(
  (result) => { 
     console.log(result);
  },
  (error) => { 
     console.log(error);
  }
);

// Success 
promise.then(
  (result) => { 
      console.log(result);
  }
);

// Error
promise.then(
  null,
  (error) => { 
      console.log(error)
  }
);
```

It is a bit odd syntax to pass a null explicitly for an error case. That's where we have an alternative called the .catch() method.

#### Exceptional things in .then() method
1. Return another promise from it
2. Return a value including undefined
3. Throw an error.

This 3 things are considered for learning the promise chain.

A promise chain fullfilling the promise of getting water to their grandparents:

```
// 1. Create a Promise to fetch the water
let promise = new Promise(function(resolve, reject) {
 // Pretend a delay of 2 sec to fetch it!
  setTimeout(function() {
      // Fetched the water. Let's resolve the promise
      resolve('Hurray! Fetched the Water.');
  }, 2000);
});

// 2. Function to Set up the handler to handle a promise result.
// It is to inform the grandparents when the result is available.
const grandParentsCooking = () => {
  // The handler function to handle the resolved promise
  promise.then(function(result) {
    // Fetched the water. Now grandparents can start the cooking
    console.log(`cooking rice with the ${result}`);
  });
}

// 3. Calling the function to activate the set up.
grandParentsCooking();
```
// About the above code:

We create the promise. In the executor function, we delay 2 seconds to pretend an async call(actually, climbing hills and fetching water takes a lot more!). Then we resolve the promise saying, 'Hurray! Fetched the Water.'

We have set up an information mechanism for the grandparents to know when the water is fetched successfully. We use the .then() handler for this purpose. Once they get the water, they start cooking. Note, here we define it, not calling it yet.

Activating the handler by calling the function.































