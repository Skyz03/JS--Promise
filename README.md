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

### .catch() Handler
You can use this handler method to handle errors (rejections) from promises. As we discussed already, it is a much better syntax to handle the error situation than handling it using the .then() method.

```
// 1. Create the promise
let promise = new Promise(function(resolve, reject) {
  setTimeout(function() {
      // Reject it as the disaster happend.
      reject(new Error('Jack fell down and broke his crown. And Jill came tumbling after.'));
  }, 2000);
});

// 2. Inform grandparents 
// but this time we are using the .catch
const grandParentsCooking = () => {
  promise.catch(function(error) {
    console.error(`OMG ${error.message}`);
  });
}

// 3. Call the function
grandParentsCooking();
```
The Output
![image](https://user-images.githubusercontent.com/42742924/156977396-9dc8cfd6-ae61-4f1e-a578-45458ce738de.png)

**Note:**
1. We use the reject method in the above code to reject the promise.
2. You can pass any type of argument to the reject method like the resolve method. However, it is recommended to use the Error objects. We will discuss it in detail in the future article on error handling with promise.
3. We use the .catch() handler to handle the rejection. In the real world, you will have both .then() and .catch() methods to handle the resolve and reject scenarios. We will learn it in the promise chaining article of the series.

### .finally Handler:
The .finally() handler method performs cleanups like stopping a loader, closing a live connection, and so on. Irrespective of whether a promise resolves or rejects, the .finally() method will be called. 
```
let loading = true;
loading && console.log('Loading...');

// Getting the promise
promise = getPromise();

promise.finally(() => {
    loading = false;
    console.log(`Promise Settled and loading is ${loading}`);
}).then((result) => {
    console.log({result});
});
```
The vital point to note, the .finally() method passes through the result or error to the next handler, which can call a .then() or .catch() again. It is convenient.

### In summary:

1. Promise is an important building block for the asynchronous concept in JavaScript.
2. You can create a promise using the constructor function.
3. The constructor accepts an executor function as an argument and returns a promise object.
4. A promise object has two internal properties, state and result. These properties are not code-accessible.
5. The consumer of a promise can use the .then(), .catch(), and .finally() methods to handle promises.
6. The Promise is better understood using examples, like the Jack and Jill Story.


## Promise Chain - The art of handling promises
This three handler methods, .then(), .catch(), and .finally(). These methods help us in handling any number of asynchronous operations that are depending on each other. For example, the output of the first asynchronous operation is used as the input of the second one, and so on.

We can chain these handlers to pass value/error from one promise to another.
There are 5 rules to understand and follow to get a grip on the chain.

### Rule 1
Every promise gives you a .then() handler method. Every rejected promise provides you a .catch() handler.
We call the .then() method to handle the resolved value.
We can handle the rejected promse with the .catch() handler

```
// Create a Promise
let promise = new Promise(function(resolve, reject) {
    reject(new Error('Rejecting a fake Promise to handle with .catch().'));
});

// Handle it using the .then() handler
promise.catch(function(value) {
    console.error(value);
});
```

Output:
Error: Rejecting a fake Promise to handle with .catch().

### Rule 2

You can do mainly three valuable things from the .then() method, return another promise(for async operation), return any other value from a synchronous operation. Lastly, throw an error.

1. Return a promise from the .then() handler
You can return a promise from a .then() handler method. You will go for it when you have to initiate an async call based on a response from a previous async call. 

```
// Create a Promise
let getUser = new Promise(function(resolve, reject) {
    const user = { 
           name: 'John Doe', 
           email: 'jdoe@email.com', 
           password: 'jdoe.password' 
     };
   resolve(user);
});

getUser
.then(function(user) {
    console.log(`Got user ${user.name}`);
    // Return a Promise
    return new Promise(function(resolve, reject) {
        setTimeout(function() {
            // Fetch address of the user based on email
            resolve('Bangalore');
         }, 1000);
    });
})
.then(function(address) {
    console.log(`User address is ${address}`);
});
```
We return the promise from the first .then() method.

Output is: 
```
Got user John Doe
User address is Bangalore
```

2. Return a simple value from the .then() handler

In many situations, you may not have to make an async call to get a value. You may want to retrieve it synchronously from memory or cache. You can return a simple value from the .then() method than returning a promise in these situations.

Take a look into the first .then() method in the example below. We return a synchronous email value to process it in the next .then() method.

```
// Create a Promise
let getUser = new Promise(function(resolve, reject) {
   const user = { 
           name: 'John Doe', 
           email: 'jdoe@email.com', 
           password: 'jdoe.password' 
    };
    resolve(user);
});

getUser
.then(function(user) {
    console.log(`Got user ${user.name}`);
    // Return a simple value
    return user.email;
})
.then(function(email) {
    console.log(`User email is ${email}`);
});
```

Output is:

```
Got user John Doe
User email is jdoe@email.com
```

3. Throw an error from .then() handler

You can throw an error from the .then() handler. If you have a .catch() method down the chain, it will handle that error. If we don't handle the error, an unhandledrejection event takes place. It is always a good practice to handle errors with a .catch() handler, even when you least expect it to happen.

In the example below, we check if the user has HR permission. If so, we throw an error. Next, the .catch() handler will handle this error.

```
let getUser = new Promise(function(resolve, reject) {
    const user = { 
        name: 'John Doe', 
        email: 'jdoe@email.com', 
        permissions: [ 'db', 'hr', 'dev']
    };
    resolve(user);
});

getUser
.then(function(user) {
    console.log(`Got user ${user.name}`);
    // Let's reject if a dev is having the HR permission
    if(user.permissions.includes('hr')){
        throw new Error('You are not allowed to access the HR module.');
    }
    // else resolve as usual
})
.then(function(email) {
    console.log(`User email is ${email}`);
})
.catch(function(error) {
    console.error(error)
});
```

Output is:

Got user John Doe
Error: You are not allowed to access the HR module.

### Rule 3:
You can rethrow from the .catch() handler to handle the error later. In this case, the control will go to the next closest .catch() handler.

In the example below, we reject a promise to lead the control to the .catch() handler. Then we check if the error is a specific value and if so, we rethrow it. When we rethrow it, the control doesn't go to the .then() handler. It goes to the closest .catch() handler.

```

// Craete a promise
var promise = new Promise(function(resolve, reject) {
    reject(401);
});

// catch the error
promise
.catch(function(error) {
    if (error === 401) {
        console.log('Rethrowing the 401');
        throw error;
    } else {
        // handle it here
    }
})
.then(function(value) {
    // This one will not run
    console.log(value);
}).catch(function(error) {
    // Rethrow will come here
    console.log(`handling ${error} here`);
});
```

Output is:

Rethrowing the 401
handling 401 here

## Rule 4
Unlike .then() and .catch(), the .finally() handler doesn't process the result value or error. It just passes the result as is to the next handler.

```
// Create a Promise
let promise = new Promise(function(resolve, reject) {
    resolve('Testing Finally.');
});

// Run .finally() before .then()
promise.finally(function() {
    console.log('Running .finally()');
}).then(function(value) {
    console.log(value);
});
```
Output is:
```
Running .finally()
Testing Finally.
```

## Rule 5
Calling the .then() handler method multiple times on a single promise is NOT chaining.

A Promise chain starts with a promise, a sequence of handlers methods to pass the value/error down in the chain. But calling the handler methods multiple times on the same promise doesn't create the chain.

![image](https://user-images.githubusercontent.com/42742924/156983465-3c7cdc83-6c64-4a48-89f7-88037d0daa37.png)

```
// This is not Chaining Promises

// Create a Promise
let promise = new Promise(function (resolve, reject) {
  resolve(10);
});

// Calling the .then() method multiple times
// on a single promise - It's not a chain
promise.then(function (value) {
  value++;
  return value;
});
promise.then(function (value) {
  value = value + 10;
  return value;
});
promise.then(function (value) {
  value = value + 20;
  console.log(value);
  return value;
});
```

The answer is 30. It is because we do not have a promise chain here. Each of the .then() methods gets called individually. They do not pass down any result to the other .then() methods. We have kept the console log inside the last .then() method alone. Hence the only log will be 30 (10 + 20). You interviewers love asking questions like this 😉!

### In summary

1. Every promise gives you a .then() handler method. Every rejected promise provides you a .catch() handler.
2. You can do mainly three valuable things from the .then() method. You can return another promise(for async operation). You can return any other value from a synchronous operation. Lastly, you can throw an error.
3. You can rethrow from the .catch() handler to handle the error later. In this case, the control will go to the next closest .catch() handler.
4. Unlike .then() and .catch(), the .finally() handler doesn't process the result value or error. It just passes the result as is to the next handler.
5. Calling the .then() handler method multiple times on a single promise is NOT chaining.

## Story of the pizza boy:

![image](https://user-images.githubusercontent.com/42742924/156984129-5618fde8-44e2-4a3a-89f7-9875482fcbd0.png)

## Async & Await keywords:

Async is used to return a promise.
Await is used to wait and handle a promise.

The async keyword is for a function that is supposed to perform an asynchronous operation. It means the function may be taking a while before it finishes execution, returns a result, or throw an error. It can either finish the execution, return result or throw an error.

```
// Example
async function fetchUserDetails(userId) {
    // pretend we make an asynchronous call
   // and return the user details
   return {'name': 'Robin', 'likes': ['toys', 'pizzas']};
}


const fetchUserDetails = async (userId) => {
   // pretend we make an asynchronous call
  // and return the user details
  return {'name': 'Robin', 'likes': ['toys', 'pizzas']};
}

```

When we invoke a async function it returns a promise. the major difference between async function and regular is ...async always returns the promise.
if you do not return a promise explicitly from an async function, JavaScript automatically wraps the value in a Promise and returns it.

The await keyword is for making the JavaScript function execution wait until a promise is settled(either resolved or rejected) and value/error is returned/thrown. As the fetchUserDetails async function returns a promise, let us handle it using the await keyword.

```
const user = await fetchUserDetails();
console.log(user)


// OR
fetchUserDetails().then((user) => console.log(user));
```

### Rules about async & await

1. You can not use the await keyword in a regular, non-async function. JavaScript engine will throw a syntax error if you try doing so.

```
function caller() {
 // Using await in a non-async function.
 const user = await fetchUserDetails();
}

// This will result in an syntax error
caller();
```

2. The function you use after the await keyword may or may not be an async function. There is no mandatory rule that it has to be an async function. Let's understand it with the following examples,

Create a non-async function that returns the synchronous message, say, Hi.
```
function getSynchronousHi() {
  return 'Hi';
}
```

You can still use the keyword await while invoking the above function.

```
async function caller() {
  const messageHi = await getSynchronousHi();
  console.log( messageHi);
}

caller(); // Output, 'Hi' in the console.
```
As you see, we can use the await with a non-async function but, we can not use it within(or inside) a non-async function.












