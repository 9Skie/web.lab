JavaScript is the programming language of the web. It can calculate, manipulate and validate data, update and change both HTML and CSS.

With javascript, we can change the color of this lightbulb (changing images).

![[Adobe Express - Screen Recording 2026-06-09 at 5.28.16 PM.gif|500]]

By default, javascript doesn't have a lot of data types, just 5:
- Boolean (true, false)
- Number (12, 1.618, -46.7, 0, etc.)
- String (“hello”, “world!”, “12”, “”, etc.)
- Null
- Undefined

In assumption you know some basic programming, like with python, javascript isn't that far off from one of them, most things that work in python works in javascript.

![[Screenshot 2026-06-09 at 5.49.32 PM.png|500]]

Except equal signs, in javascript they use `===` for equals. Why? In JavaScript, `==` performs type coercion (i.e. forces the arguments to be of the same type before comparing them).

![[Screenshot 2026-06-09 at 5.51.24 PM.png|400]]

But in terms of syntax, javascript looks a lot like C for some reason...
- you need a `;` at the end of each line
- you wrap functions around in `{}`
- comments are in `//`

![[Screenshot 2026-06-09 at 6.06.52 PM.png|500]]


For variables we don't change, we use `const`, for variables we do change, we use `let`.

![[Screenshot 2026-06-09 at 6.10.01 PM.png|200]]


There's also not assigned values, for `undefined` it's an empty variable that can be assigned later, while `null` is just... no value...

![[Screenshot 2026-06-09 at 6.09.09 PM.png|400]]


To print something out, you use `console.log()`, which is the JavaScript equivalent of Python's `print()` or C's `printf()`,  it outputs whatever you give it to the browser's developer console.

```js
console.log("Hello");        // prints a string
console.log(42);             // prints a number
```

However,  `print()` in Python sends output to the terminal/stdout, while `console.log()` sends output to the DevTools console, so regular users never see it.


Arrays are very similar to python, no limit to data types, and you can push and pop.

![[Screenshot 2026-06-09 at 8.51.14 PM.png|500]]


Javascript (if, while, for) looks basically like C.

However, javascript doesn't have 'classes', it however does again, have something that looks remarkably like C.

This is C.

![[Pasted image 20260609210001.png|300]]

This is javascript.

![[Screenshot 2026-06-09 at 9.00.55 PM.png|300]]

You access it through a similar fashion to C as well, but also this python-ish syntax of `[]`.

![[Screenshot 2026-06-09 at 9.04.49 PM.png|400]]


And javascript has something weird, despite the values in these 2 different arrays/objects being the same, javascript still returns comparing them equal as false.

![[Screenshot 2026-06-09 at 9.20.30 PM.png|500]]

Reasoning being, they are 2 different objects with the same values living in different places in memory, so... javascript says nah.,

![[Screenshot 2026-06-09 at 9.22.28 PM.png|300]]

So, if we want them to be equal, we must have the other variable pointing over to the same location in memory.

![[Screenshot 2026-06-09 at 9.24.27 PM.png|400]]

But uh... this raises the new question, if I edit a property of this object for variable 1, it would also affect variable 2's values, since they are fundamentally looking at the same place in memory.

So you can use the spread operator `...` and copy things over.

![[Screenshot 2026-06-09 at 9.26.50 PM.png]]


