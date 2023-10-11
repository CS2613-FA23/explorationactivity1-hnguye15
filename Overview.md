# Package/Library Overview
## Package/Library
Instead of using a package or a library, I have found good usage in a particular utility module called "Async.js". Moreover, this module will be used in conjunction with the Promise object to simulate time-related functions. 

## Async.js
### Purpose
Async.js utility module is primarily used to perform asynchronous programming. According to Mozilla.org, "asynchronous programming is a technique that enables your program to start a potentially long-running task and still be able to be responsive to other events while that task runs, rather than having to wait until that task has finished. Once that task has finished, your program is presented with the result [[ref]](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Asynchronous/Introducing)." For this program, the module is mainly used to handle multiple tasks in the background while updating progress in the foreground.

### Usage
More from Mozilla.org, "The async function declaration creates a binding of a new async function to a given name. The await keyword is permitted within the function body, enabling asynchronous, promise-based behavior to be written in a cleaner style and avoiding the need to explicitly configure promise chains [[ref]](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/async_function)." To define an async function, simply type "async" in the front of function declaration. As a result, the syntax for this is as simple as:

    async function functionName(param0, param1, ..., paramN) {
        statements
    }

While asynchronous functions can be declared using "async" to return a promise, they also must be called with "await" to wait for such promise.

An example of async module working with the promise object to simulate the sleep() function from C:

    async function sleep(ms) {
        return new Promise(resolve => setTimeout(resolve, ms));  
    }
    
    console.log('The pie's gonna be ready in 7 years! Give it some time~');
    await sleep(220752000000);
    console.log("You can have the pie now :D");

For this code example, you can wait exactly 7 years for a delicious pie. But hey, if it's worth it, it's worth it.

Consequently, the entirety of the program will be mainly revolving around this one function to simulate in-game delays.

### Functionality
According to Mozilla.org, "An async function declaration creates an AsyncFunction object. Each time when an async function is called, it returns a new Promise which will be resolved with the value returned by the async function, or rejected with an exception uncaught within the async function [[ref]](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/async_function)."

Further, "Async functions can contain zero or more await expressions. Await expressions make promise-returning functions behave as though they're synchronous by suspending execution until the returned promise is fulfilled or rejected. The resolved value of the promise is treated as the return value of the await expression. Use of async and await enables the use of ordinary try/catch blocks around asynchronous code [ref]](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/async_function)."

#### Example
    function resolveAfter2Seconds() {
      console.log("starting slow promise");
      return new Promise((resolve) => {
        setTimeout(() => {
          resolve("slow");
          console.log("slow promise is done");
        }, 2000);
      });
    }
    
    function resolveAfter1Second() {
      console.log("starting fast promise");
      return new Promise((resolve) => {
        setTimeout(() => {
          resolve("fast");
          console.log("fast promise is done");
        }, 1000);
      });
    }
    
    async function sequentialStart() {
      console.log("== sequentialStart starts ==");
    
      // 1. Start a timer, log after it's done
      const slow = resolveAfter2Seconds();
      console.log(await slow);
    
      // 2. Start the next timer after waiting for the previous one
      const fast = resolveAfter1Second();
      console.log(await fast);
    
      console.log("== sequentialStart done ==");
    }
    
    async function sequentialWait() {
      console.log("== sequentialWait starts ==");
    
      // 1. Start two timers without waiting for each other
      const slow = resolveAfter2Seconds();
      const fast = resolveAfter1Second();
    
      // 2. Wait for the slow timer to complete, and then log the result
      console.log(await slow);
      // 3. Wait for the fast timer to complete, and then log the result
      console.log(await fast);
    
      console.log("== sequentialWait done ==");
    }
    
    async function concurrent1() {
      console.log("== concurrent1 starts ==");
    
      // 1. Start two timers concurrently and wait for both to complete
      const results = await Promise.all([
        resolveAfter2Seconds(),
        resolveAfter1Second(),
      ]);
      // 2. Log the results together
      console.log(results[0]);
      console.log(results[1]);
    
      console.log("== concurrent1 done ==");
    }
    
    async function concurrent2() {
      console.log("== concurrent2 starts ==");
    
      // 1. Start two timers concurrently, log immediately after each one is done
      await Promise.all([
        (async () => console.log(await resolveAfter2Seconds()))(),
        (async () => console.log(await resolveAfter1Second()))(),
      ]);
      console.log("== concurrent2 done ==");
    }
    
    sequentialStart(); // after 2 seconds, logs "slow", then after 1 more second, "fast"
    
    // wait above to finish
    setTimeout(sequentialWait, 4000); // after 2 seconds, logs "slow" and then "fast"
    
    // wait again
    setTimeout(concurrent1, 7000); // same as sequentialWait
    
    // wait again
    setTimeout(concurrent2, 10000); // after 1 second, logs "fast", then after 1 more second, "slow"

## Origin
Asynchronous programming was implemented by the language F# first then from there on, a lot more languages have started to adopt this programming style, especially C#, which was the first mainstream language that popularized the async/await keywords [[ref]](https://dev.to/maxarshinov/a-brief-history-of-asyncawait-264j).

As for the Promise object used alongside the module, according to risingstack.com, "the current JavaScript Promise specifications date back to 2012 and available from ES6 – however Promises were not invented by the JavaScript community. The term comes from Daniel P. Friedman from 1976 [[ref]](https://blog.risingstack.com/asynchronous-javascript/)."

## Reasons for Selection
At the start of this term, I had a small passion project that was brewing in my thoughts even during last Summer. So, I told myself "why not sit down and learn something new that you like?". From then on, I have been following a series of video on Youtube on how to make a web-based incremental game like Cookie Clicker as a base for my game ([link to the series](https://www.youtube.com/playlist?list=PLEyTwruuVAqlEvj8QxTFdVPc6_AwpgF2w)). The game is a combination of HTML and JavaScript: HTML for the front-end presentation, and JavaScript for the back-end handling of logics. I also planned to add CSS to the game for better graphics, but I digress. At first, I never had the intention of using this game for my first exploration activity in this class, but because of how much we learn about JavaScript in this class and the code of my game is also mainly written with JavaScript, I found that it was a perfect candidate for this opportunity to showcase my game.

As I continued further down the development line, I stumbled upon asynchronous programming (AP), namely, JavaScript's Async.js utility module. AP at first was very confusing for me with the async/await thing, but as I took more time familiarizing myself with the module and work with it, it started to become clearer to me. Although I felt like I only learned a small corner of the module, I am proud that it is something I can put into great use in the future for my other projects not just as games. For the development of my game, instead of sticking to a traditional clicker incremental game, I leaned towards more its idle sub-genre that involves a very lot of automations and multiple tasks running in the background. This is where the Async.js module shines the brightest! By using this module, I feel that coding my game is much easier and simpler while still able to maintain efficiency.

## The Learning Curve
Personally, all of the struggle working with this particular language really did pay off for me because I learn a lot from making mistakes and I cannot emphasize on this enough. At first, I would go blind into the language, then figure things out in bits and pieces. Debugging is a very common thing when you learn a new language because of how many errors you make because of difference in syntax, logic, and other resources like libraries and things alike. But, as you learn and make more mistakes, it slowly grows onto you. For example, at first, I literally had no idea how this Async.js utility module works. I basically went ahead and used it blindly until there were a lot of errors popping up that I had to resolve. So, I would say that looking at the bugs from your code and figuring them out yourself plays a huge role in learning, especially when there's nobody there to point them out for you because it's your code after all and nobody knows your code more than you do. As such, implementing the module and understanding it was quite a challenge, but was a very successful challenge. Now I mostly know how to program asynchronously and handle multiple tasks in the background to aid with the tasks in the foreground.

## Personal Experience
Overall, I would totally recommend this type of programming to everyone as it is a very useful one. I also bet that asynchronous programming is very widely used and very heavily implemented in many programs. It is something that everyone should at least have their experience with at least once as a programmer.

On a side note, I will probably be working more with this module in the future. Maybe, I will hopefully finish developing the game with many more features to come!
