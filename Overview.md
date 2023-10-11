# Package/Library Overview
## Package/Library
Instead of using a package or a library, I have found good usage in a particular utility module called "Async.js". Moreover, this module will be used in conjunction with the Promise object to simulate time-related functions. 

## Async.js
### Purpose
Async.js utility module is primarily used to perform asynchronous programming. According to Mozilla.org, "asynchronous programming is a technique that enables your program to start a potentially long-running task and still be able to be responsive to other events while that task runs, rather than having to wait until that task has finished. Once that task has finished, your program is presented with the result [ref](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Asynchronous/Introducing)." For this program, the module is mainly used to handle multiple tasks in the background while updating progress in the foreground.

### Usage
More from Mozilla.org, "The async function declaration creates a binding of a new async function to a given name. The await keyword is permitted within the function body, enabling asynchronous, promise-based behavior to be written in a cleaner style and avoiding the need to explicitly configure promise chains [ref](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/async_function)." To define an async function, simply type "async" in the front of function declaration. As a result, the syntax for this is as simple as:

    async function functionName(param0, param1, ..., paramN) {
        statements
    }

Asynchronous functions must be called with "await" to work as intended.

An example of async module working with the promise object to simulate the sleep() function from C:

    async function sleep(ms) {
        return new Promise(resolve => setTimeout(resolve, ms));  
    }
    
    console.log('The pie's gonna be ready in 7 years! Give it some time~');
    await sleep(220752000000);
    console.log("You can have the pie now :D");

For this code example, you can wait exactly 7 years for a delicious pie. But hey, if it's worth it, it's worth it.

Consequently, the entirety of the program will be mainly revolving around this one function to simulate in-game delays.
