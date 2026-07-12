If you recall from the 3rd class:

(show them this part)

This class is mostly related to javascript callback functions. A callback function is just a function you pass as an argument to _another_ function, to be run later.

For example, this function:

```js
setTimeout(function() {
    console.log("1 second passed");
}, 1000);
```

`setTimeout` takes a function and says "I'll call this back to you after 1 second."

As for why this is a thing in javascript... it's because javaScript is a single-threaded programming language, it can only do one thing at a time.

So instead of waiting, you pass a callback and say "call me when you're done."

---

At this point now in time, a lot of our processes aren't just natively running javascript, we call for frontend calls services from the servers, our servers goes to call APIs or reach to our databases, and all these operations take time.

These operations (called requests) that we wait on are called promises, and they will have 1 of 3 statuses possible:
- Fulfilled
- Pending
- Rejected

Like here, we are calling a request to an API for 'ordering kitties'

![[Screenshot 2026-07-05 at 11.28.56 AM.png|500]]

Once the promise is fulfilled, we can act on this returned promise object, like hugging the cats.

![[Screenshot 2026-07-05 at 11.37.48 AM.png|500]]

Once the promise is rejected, we need to use a catch function to tell us something went wrong (or handle it).

![[Screenshot 2026-07-05 at 11.39.07 AM.png|500]]

But, as we recall that Javascript is a single threaded programming language, we can't both send requests & do other things at the same time, but it's not really smart to waste time and just sit around either, so Javascript has this idea of `async`.

(show them this part)

What JavaScript calls "async" is really just task scheduling on a single thread:

```
CUDA:     Thread 1  ████████████████
          Thread 2  ████████████████
          Thread 3  ████████████████
                    ← all running at once →

JavaScript:         ████████░░███░░░███░░████
                    ← one thread, doing one thing at a time,
                      queuing the rest to run later →
```

Basically parallel programming on a toddler bicycle with support wheels.
- Smirk

---

Now that we understand it in concept, lets see it actually running in code.

We start by asynchronously calling a function that returns a promise.

![[Screenshot 2026-07-05 at 2.29.43 PM.png|500]]

Then we define a callback function of what to do when the function returns a successful promise.

![[Screenshot 2026-07-05 at 2.33.31 PM.png|500]]

While we wait, we can go do some other tasks & things in javascript.

![[Screenshot 2026-07-05 at 2.35.59 PM.png|500]]

Now, how would the output of this function look like? As you expect, it first returns the instant `console.log()` lines, and then returns the callback function's outputs (more console.log lines).

![[Screenshot 2026-07-05 at 2.42.43 PM.png|500]]

---
## Lots of Promises 

It does get a bit confusing when we have more than 1 promise going on at the same time, like for example, we can't compute with pending promises.

![[Screenshot 2026-07-05 at 2.49.37 PM.png|300]]

So right here, JS doesn’t know what a and b are when it does this addition. It just sees 2 pending promises. It doesn't wait for the promises to resolve before continuing, it just puts `[object Promise][object Promise]`.

There's also ways to deal with many promises simultaneously in a list, like `Promise.race()`, `Promise.all()`, `Promise.any()`...

- `Promise.all`: waits for all 5, gives all 5 results in order. If any one fails, the whole thing rejects and you get nothing. Natural fit here since you want every comment thread.
- `Promise.allSettled`: waits for all 5, never rejects; each result says fulfilled or rejected. Use when one failed thread shouldn't kill the other four.
- `Promise.race`: settles with whichever finishes first, success or failure. Mostly used to race a fetch against a timeout.
- `Promise.any`: resolves with the first success, ignoring failures; only rejects if all 5 fail. Use for redundant sources.

---
## Asynchronous Vs Synchronous

Again, easy peasy lemon squeezy if you look ever into parallel computing, lets begin with some of the easy assumptions.

Suppose that:
- the red block of code depends on the orange & green block
- the orange block must run before the red block
- the green block must run before the red block

In typical javascript, it can look anything like this:

![[Screenshot 2026-07-05 at 3.05.23 PM.png|500]]

If we could offload the work from the orange block to some other computer, the program would take 4 time units.

![[Screenshot 2026-07-05 at 3.05.53 PM.png|500]]

So, we just saw this 'stall' in order to wait for 2 and 3 to all be resolved to use their values.

Similar to this previous example, JS doesn’t know what a and b are when it does this addition. It just sees 2 pending promises.

![[Screenshot 2026-07-05 at 2.49.37 PM.png|300]]

We can use a keyword called `await` for javascript to await for a and b's values to be resolved, then use that value.

![[Screenshot 2026-07-05 at 3.07.43 PM.png|500]]

However, only asynchronous functions can use await, remember that, and to make a function to be async, we just add the word 'async' into our function so then we can use await.

![[Screenshot 2026-07-05 at 3.50.06 PM.png|500]]

Using async await notation to perform a get request in useEffect requires us to define and call an async function inside the callback function passed to useEffect

![[Screenshot 2026-07-05 at 3.51.29 PM.png|500]]

So, TLDR is use async + wait!

---
## Async Under The Hood

How does Javascript decide when to run callback functions after a promise is fulfilled? Wouldn’t it cause problems to randomly call a callback function while we are going through the synchronous parts of our program? 

Fortunately, the javascript event loop controls the logic necessary to make async calls work correctly.

How it works is that whenever a promise is fulfilled, the callback function associated with that promise is added to a task queue. Functions on the task queue are executed only when the call stack is clear.
- It's almost like how computer architecture works... how fascinating

![[Screenshot 2026-07-05 at 3.56.25 PM.png|500]]