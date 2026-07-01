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

```js
console.log("Starting...");

setTimeout(() => {
    console.log("5 seconds later");
}, 5000);

console.log("Still running while we wait!");
// Output:
//   "Starting..."
//   "Still running while we wait!"
//   (5 seconds later) "5 seconds later"
```

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

JavaScript can do I/O in the background (the browser/node handles network requests on separate threads), but your JavaScript code itself never runs two functions at the same time.


Another way to look at callbacks is using it somewhat like python's `map` functions, you can pass functions to functions as well.

Take a look at this code, it takes an array of celsius numbers, and converts them into Fahrenheit.

![[Screenshot 2026-06-10 at 12.07.15 PM.png|400]]

But what if I want not just one conversion, but all three?

- Celsius → Fahrenheit
- Fahrenheit → Celsius  
- Celsius → Kelvin

Only the formula changes, the iteration (looping through the array) stays the same.

![[Screenshot 2026-06-10 at 3.46.41 PM.png|500]]

So why not pass the formula itself as a parameter? A callback also does that too,  passing a function as an argument to another function.

![[Screenshot 2026-06-10 at 3.45.52 PM.png|500]]

```js
// General function — takes an array and a formula function
const convertArray = (arr, formula) => {
    let result = [];
    for (let i = 0; i < arr.length; i++) {
        result.push(formula(arr[i]));  // formula is a callback
    }
    return result;
};

// Define the formulas as separate functions
const cToF = (temp) => temp * 9/5 + 32;
const fToC = (temp) => (temp - 32) * 5/9;
const cToK = (temp) => temp + 273.15;

// Pass the formula into the general function
convertArray([0, 100], cToF);     // [32, 212]
convertArray([32, 212], fToC);    // [0, 100]
convertArray([0, 100], cToK);     // [273.15, 373.15]
```

In JavaScript, functions can be passed around like any other value (numbers, strings, etc.). This is very similar to Python's `map` function:

```python
list(map(lambda x: x * 9/5 + 32, [0, 100]))  
# [32, 212]
```

In fact, JavaScript arrays have their own `.map()` method that does exactly this, you can pass the callback inline:

```js
[0, 100].map(temp => temp * 9/5 + 32);
// [32, 212]
```


Now, when you have map, you have filter, it's the exact same idea as map, except it's for, as you guessed it, filtering.

`.filter()` takes a callback that returns `true` or `false`, if `true`, the element stays, if `false`, it's removed.

```js
let nums = [3, -6, 2, 0, -9, 4];
let positive = nums.filter(x => x > 0); 
// [3, 2, 4]
```

Compared to Python:

```python
# Python
nums = [3, -6, 2, 0, -9, 4]
positive = list(filter(lambda x: x > 0, nums))
# [3, 2, 4]
```

Same idea, loop through the array, keep what matches the condition.