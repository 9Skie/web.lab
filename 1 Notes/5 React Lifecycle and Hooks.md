Now that we saw React as a way to modularize components and make visuals more reusable, there's one more thing we need: changing what is shown in response to interactions (states). This class is entirely about how state changes.

Last time, we didn't give state a proper introduction.

React functional components use the `useState` hook to hold state. Each `useState` call creates a state variable and a setter function. When you call the setter, React re-renders the component.

To create state, we write:

```js
const [value, setValue] = useState(initialValue)
```

This is array de-structuring. `useState(initialValue)` always returns an array of two things:

```
[currentValue, setterFunction]
```

So the code above is equivalent to:

```js
const stateArray = useState(initialValue)
const value = stateArray[0]      // the current value
const setValue = stateArray[1]   // the function to update it
```

You name them whatever makes sense for your data. If the state is a person's name, you'd write:

```js
const [name, setName] = useState("Alice")
```

![[Screenshot 2026-06-23 at 11.13.34 PM.png|500]]


Here are 3 examples

![[Screenshot 2026-06-23 at 11.13.55 PM.png|500]]

1. We pass the initial value of the state variable into `useState`. Example: `useState(0)` starts count at 0.
2. `useState` returns an array. Position 0 is the current value (e.g. `persons`); position 1 is the setter function to update it (e.g. `setPersons`).
3. Call the setter when something happens (click, scroll, etc.). React re-renders and the component sees the new value.


Now let's look at an example. Both tweet panels look structurally the same, but clicking the `Likes` tab should switch the content to show only liked posts. Clicking `Posts` switches back. The active tab is stored in state, and clicking a tab calls the setter to change it, which re-renders the tab panel with the new content.

But, the big purple chunk below it, `<TweetPanel />` , which should hold the according information to the tab we are on, doesn't change when we change tabs. 
- They're siblings, and neither can see the other's state. So clicking a tab doesn't change the panel.

![[Screenshot 2026-06-23 at 11.42.43 PM.png|500]]

So the question (as stated in the picture) is how can we change the content in `<TweetPanel />` shows when we change `<Tabs />` content? 

![[Screenshot 2026-06-24 at 7.41.19 AM.png|500]]

In the current way as we know it in React... we can't! We have to get creative and give their states into a `shared state` into it's parent, `<Feed />`.

Instead of each child owning its own state, the parent `<Feed />` holds the state and passes it down to both:

![[Screenshot 2026-06-24 at 7.39.37 AM.png|500]]

In the fixed version, there's one state variable in Feed. `selectedTab` gets set by `Tabs` (via setSelectedTab), and `TweetPanel` just reads the value as a prop. One source of truth, both children react to it.

So, when siblings need to share data, put the state in their closest common parent and pass it down as props. As you cannot edit a component’s state from another component! The whole point of separating code into components is to keep states independent of each other. 


We'll take a look at another example while we are at it, recall the facebook app page:

![[Screenshot 2026-06-24 at 7.55.12 AM.png|500]]

What do we actually need to pass down from `<App />`, and what do we not need to pass down from it?

![[Screenshot 2026-06-24 at 7.54.48 AM.png|500]]

Well... everything but list of tweets, as `<Feed />`, `<Trending />`, and `<Suggestions />` have many things in common.

- Feed needs to see who you follow and who you blocked
- Trending needs to see who you follow, who follow you, (and who you blocked)
- Suggestions need to see who you follow, who follow you, and who you blocked.

![[Screenshot 2026-06-24 at 7.59.33 AM.png|500]]

---
## The State Life Cycle

Beyond just changing state and updating visuals, there's more we can do with components!

Each component in React has a lifecycle with three main phases: **Mounting**, **Updating**, and **Unmounting**.


Let's start with mounting, think of it like a restaurant kitchen:

1. Trigger: The waiter gives an order to the kitchen. This is the first time a component needs to show up on screen, and never again.

2. Render: The chef (React) runs the JavaScript code inside the component and its subcomponents, cooking up what to display. The result (JSX) is handed back to the waiter.

3. Commit: React takes the returned JSX and puts it into actual HTML on the page. The dish is served to the viewer.

![[Screenshot 2026-06-24 at 7.14.35 PM.png|500]]



Look at this page, where we just have this bare bone 'Welcome to the web.lab Restaurant' and a button that says 'Order Steak'.

![[Screenshot 2026-06-24 at 8.09.48 PM.png|400]]

When we click the button 'Order steak', as you might have guessed, a steak pops up!

![[Screenshot 2026-06-24 at 8.17.05 PM.png|400]]


Now, we just ran through the entire step of mounting! What just happened? Let's go through it.

we just activated the `trigger` for mounting this state, as `<Steak />` component is called for the first time.

![[Screenshot 2026-06-24 at 8.22.21 PM.png|500]]

Then react has to go run the Javascript code in the `<Steak />` component.

![[Screenshot 2026-06-24 at 8.22.38 PM.png|500]]

And then we finally come to actually commit and showing the updated steak to the user.

![[Screenshot 2026-06-24 at 9.03.46 PM.png|500]]

Btw, beneath there in the commit exists something called a `HTML DOM updated`, don't worry about it for now, you can just think it as the place where the commit goes, it's where the dish gets served, where React is updating the browser's actual HTML. 

So, it's absolutely nothing crazy. We've seen this similar idea exactly in JavaScript, just how as JavaScript's entire purpose is to dynamically update webpages. This is just how React names the process of doing something similar.

Once the component is mounted, we can show different states of it too. Clicking "send back to kitchen" sends a note back to the chef to cook the steak further, so React knows to re-render this component with a new value. In this vase, going from raw to a rare steak.

![[Screenshot 2026-06-25 at 8.00.51 AM.png|500]]

As we can see, state is the only memory for this component, and during the render phrase, all these lines run again.
- Don't be scared, all that it is is just `doneness = doneness + 1`, re-render `image[doneness]`.

![[Screenshot 2026-06-25 at 8.31.20 AM.png|500]]

Let's keep cooking the steak! The steak goes from raw → rare → medium → burnt "congratulation" steak, and we've hit the end on how well we can cook it, the send back to kitchen button gets deleted.

![[Screenshot 2026-06-25 at 8.41.29 AM.png|400]]

In this process, we just repeatedly come to the `state change` once, `stage change` again, `state change` and another one... cycle, but here instead of mounting, the trigger is a state update.

![[Screenshot 2026-06-25 at 8.42.42 AM.png|500]]

What happens when we click the `Delete Steak` button now? The steak image is gone! We have `dismounted` the component entirely.

![[Screenshot 2026-06-25 at 8.42.21 AM.png|500]]

---
## DOM (Document Object Model)

So, previously we've got a glimpse of this thing, but what exactly is it?  

A DOM is a model representing an HTML document as a tree of objects
- Document: the entire webpage
- Object: each HTML element is treated as an object
- Model: describes the structure and content of the HTML page

Another way to understand it is that the DOM is the live representation of the page, and it's the only thing the browser actually cares about for rendering, it knows not of React.

![[Screenshot 2026-06-27 at 10.13.45 PM.png|300]]

But, just as we know that React creates these 'fake' html tags for the sake of re-usability, it also creates a 'fake', virtual DOM that represents the structure of your UI.

![[Screenshot 2026-06-27 at 10.30.35 PM.png|300]]

Now, how does this DOM interact throughout the component life cycle? Well, we start by mounting the component, which really means adding a component to the DOM.

![[Screenshot 2026-06-27 at 10.31.36 PM.png|500]]

Then whenever we have a trigger that causes the component to update, we re-render this component with the new values on the DOM.

![[Screenshot 2026-06-27 at 10.33.06 PM.png|500]]

Lastly, whenever we need this component to go, we remove it from the DOM.

![[Screenshot 2026-06-27 at 10.33.38 PM.png|500]] 


---
## React Hooks

Ah, these hooks are similar the ones we see in machine learning, where when we start x, y starts as well, or when x is done, y gets started.

Let's take a look at this function, what do you expect it to log down? We would expect `me` to be inside persons, but it's not there.

![[Screenshot 2026-06-28 at 7.49.07 AM.png|500]]

The problem is that, `setPersons` is a React state setter. It doesn't mutate the existing `persons` variable, it schedules a re-render with a new value. 

The sequence is:

1. `setPersons([...persons, "me"])` requests that on the next render, the state become `["me"]`.
2. `console.log(persons)` runs immediately, still in the current render, where `persons` is unchanged → logs `[]`.

The new value `["me"]` only becomes visible as `persons` on the _next_ render, in a fresh function call.

So, what's the fix? Hooks! Hooks allow functions to have access to state and other React features without using classes.

There's many different hooks for different scenarios, like the `useState` hook, it can track state (data) in a function component, but in this case, it's already being used by the `setPersons` syntax.

The new value only becomes visible on the next render. `useEffect` is how you run code _on_ that next render, so it's where you finally get to see and act on the updated value.

If you'd put your `console.log` inside a `useEffect` watching `persons`, it _would_ show `["me"]`:

```js
setPersons([...persons, "me"]);
console.log(persons); // [] — too early, this render

useEffect(() => {
  console.log(persons); // ["me"] — runs after the update lands
}, [persons]);
```

My god, do I have to complain of how disgusting this class was, at least this one, because there was just no good explanation on what the fuck a hook is. I hated this part, and I need to read more myself.