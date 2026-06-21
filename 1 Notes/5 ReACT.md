That names scares me, not as some frontend development framework, but as the foundational paper that began the idea of [AI agents](https://arxiv.org/abs/2210.03629).

![[Pasted image 20260610160028.png|200]]

Anyways! React is a javascript library for building user interfaces, it was developed by Meta back in 2013, and is still the most popular UI library today.
- Hm... considering Pytorch is still the most popular deep learning framework (also made by Meta), that's pretty cool

Around React there's a big ecosystem, and people have built libraries for all sorts of purposes on top of base react.

---
## Before React

We've seen the basics of the building blocks of a website UI, html, css, and javascript.

![[Screenshot 2026-06-10 at 4.23.08 PM.png|500]]

But how does javascript interact with HTML/CSS?  It's simple! In HTML, JavaScript code is inserted between `<script>` and `</script>` tags.

Once the page loads, JavaScript can access and modify HTML elements through the DOM (Document Object Model) API. The browser turns your HTML into a tree of objects that JS can read and change.

Remember the lightbulb animation that we had? That uses the `<scripts>`.

![[Adobe Express - Screen Recording 2026-06-09 at 5.28.16 PM.gif|500]]

```html
<!DOCTYPE html>
<html>
<body>
    <h2>What Can JavaScript Do?</h2>

    <p>JavaScript can change HTML attribute values.</p>

    <p>In this case JavaScript changes the value of the src (source) attribute of an image.</p>

    <button onclick="document.getElementById('myImage').src='pic_bulbon.gif'">
        Turn on the light
    </button>

    <img id="myImage" src="pic_bulboff.gif" style="width:100px">

    <button onclick="document.getElementById('myImage').src='pic_bulboff.gif'">
        Turn off the light
    </button>
</body>
</html>
```

The lightbulb example uses JavaScript written **inline** inside the HTML:

```html
<button onclick="document.getElementById('myImage').src='pic_bulbon.gif'">
```

When clicked, it:

1. Finds the `<img>` element by its ID (`myImage`)
2. Changes its `src` attribute to `pic_bulbon.gif`

Click the button and it grabs the image by its ID (`myImage`), swaps the `src` to `pic_bulbon.gif`, and the browser loads the new image.

However, this logic is splattered across `onclick` attributes. 2 different buttons each hardcode a different image URL,  10 button would have it's logic be in 10 places.


## After React

```jsx
function Lightbulb() {
    const [isOn, setIsOn] = React.useState(false);

    return (
        <div>
            <h2>What Can JavaScript Do?</h2>
            <p>JavaScript can change HTML attribute values.</p>
            <button onClick={() => setIsOn(true)}>Turn on the light</button>
            <img
                src={isOn ? "pic_bulbon.gif" : "pic_bulboff.gif"}
                style={{ width: "100px" }}
            />
            <button onClick={() => setIsOn(false)}>Turn off the light</button>
        </div>
    );
}
```

- No `getElementById`: React tracks state (`isOn`), not DOM elements
- No scattered `onclick` strings: all logic lives inside the component
- One source of truth: the image source is a single expression `isOn ? "pic_bulbon.gif" : "pic_bulboff.gif"` instead of two separate hardcoded values
- State drives the UI: when `isOn` changes, React automatically re-renders the image. You don't tell React *how* to change the DOM; you just describe what the UI should look like for each state.


Of course, the power of react doesn't end there, we'll go back into the class.

Take a look at this webpage:

![[Screenshot 2026-06-17 at 3.57.55 PM.png|500]]

If you were purely using the tools which we've been learning, how the heck would we create this webpage? It'd be a _mountain_ of divs.

On the left, the friends sidebar alone:
- a div wrapping the whole friends section
- a div for the header: friends, see friends link, number of friends....
- a div holding all the thumbnails
- and then, for every single friend: an image, a name... 

On the right, the feed. And every post is its own pile of divs:
- a div for the header: profile picture, name, timestamp...
- a div for the post text
- a div for the post's image
- a div for the comments section
- and _inside that_, a div for each comment with its own name and text...

And then you do that again. And again. For the next post, and the next...and the next ten thousand posts, this is completely unmaintainable.

Wouldn't it be so much more happier if we just had `<Facebook />` as a tag and everything that we just discussed magically appears? It would, but we would still need to build it from smaller, primitive parts.

For example, it would be nice if we can just define this facebook tag with `<NavBar />`, `<Friends />`, `<Feed />`.

![[Screenshot 2026-06-17 at 4.08.50 PM.png|200]]

Ok...? Getting somewhere, but what is `<NavBar />`, `<Friends />`, and `<Feed />`? Those are also not native HTML looking tags themselves, if we keep going down and down, we can actually build these as native HTML parts.

![[Screenshot 2026-06-17 at 5.25.19 PM.png|500]]

These customizable parts with custom names built from native html is called `components`, and they are a core concept in React.

 Fundamentally, they are fake HTML tags that bundle HTML, CSS, and JavaScript into a single file for reusability.

![[Screenshot 2026-06-17 at 5.27.09 PM.png|500]]

---
## An Example

Let's take Facebook for an example, as it's the beginning of all this mess and this chaos.

This is the main homepage component of facebook, called `<App />`.

![[Screenshot 2026-06-17 at 5.36.56 PM.png|500]]

Which, as we just recalled is broken down into `<NavBar />`, `<Friends />`, and `<Feed />`.

![[Screenshot 2026-06-17 at 5.49.22 PM.png|500]]

If we take a closer look at one of such components, such as `<Feed />`, we can see it's made of smaller components called `<Post />`. 

![[Screenshot 2026-06-17 at 5.49.38 PM.png|500]]

Going down further, a post component is made of a `<PostBody />`, `<Comment />`, `<PostBody />`.

![[Screenshot 2026-06-17 at 6.02.20 PM.png|500]]

So this goes down and down until we hit bedrock HTML, CSS, and JavaScript. This naturally makes a tree-like data structure, since there's hierarchy between components.

![[Screenshot 2026-06-17 at 6.06.39 PM.png|500]]

---
## Why Components?

The whole point of components is just reusability, giving a general template to anything visual.

![[Screenshot 2026-06-17 at 6.14.50 PM.png|500]]

But now that we have a general template, how do we know the actual individual elements that go inside each component?

![[Screenshot 2026-06-17 at 6.17.22 PM.png|500]]

In React, we call this `props`, the process of inputs passed down from a parent to a child component.

In this case, we want to pass information into a child component, `Comment` from it's parent component Post, and when the individual comment renders, it will have the data from the parent.

![[Screenshot 2026-06-17 at 6.26.00 PM.png|500]]

It's like making a class in Python. The class defines a general template for how something is supposed to be, and then we create individual objects to fill in actual instances of the class.

![[6BEB96C8-0D55-412D-BAB8-79D41610D7FE.png|200]]
- A prop is just an object of key-value pairs passed to a component

![[Screenshot 2026-06-17 at 6.34.54 PM.png|500]]

This is an example of a rendered prop. When props are passed down to the child, the child CANNOT change them. A child also cannot pass any props upwards to the parent.

![[Screenshot 2026-06-17 at 6.35.25 PM.png|500]]

---
## States

But, what if the displayed content keeps changing? Like if people make new comments, how do we keep track of those changes? A prop is a dead thing that can't change over time.

This is where states come in, a state is a component's own private, changeable memory. Props come from a parent and the component can't change them; state lives inside the component and the component _can_ change it.

It's information maintained by a component that controls what gets displayed, and unlike props it can be updated by human inputs (button clicks) or computer inputs (network responses).

Say, in this example of comments under a post, our state could be keeping track of a list of comments, and sending the props of a specific comment to the `<Comment />` child when needed.

![[Screenshot 2026-06-17 at 10.05.08 PM.png|400]]

Then it's by some decision that we pick and choose which comment to render! Maybe it's the latest uploaded comment, or the most popular comment, who knows?

![[Screenshot 2026-06-17 at 10.07.37 PM.png|300]]

---
## An Actual Example

While we visually see the idea of React, we have 0% understanding of how to actually work with it. We theoretically know what's the point of React, but we have never ever touched React yet.

So... what we waiting around for? Let's go! Say we are trying to make this little components of a comment.

![[Screenshot 2026-06-19 at 5.36.24 PM.png|300]]

By default, it's just a name + a content.

![[Screenshot 2026-06-19 at 5.38.01 PM.png|300]]

And in using React, we have to import the library, define the component, and export it.

![[Screenshot 2026-06-21 at 10.24.28 AM.png|500]]

As for the body of the component... it's just like a function, right? It should take in the props, the data, and output it in some format that we want, in this case the comment.

![[Screenshot 2026-06-21 at 10.26.47 AM.png|500]]

And so, assuming we set up the props correctly, all we need to do is return a div, with html inside.
- The reason it's all inside a div is because javascript functions only allows you to return 1 thing, and so... we just stuff everything inside a div.

![[Screenshot 2026-06-21 at 10.32.38 AM.png|500]]

Also... it's not returning html! If you look carefully, it's something else called JSX, which if we recall what a prop is, it's just a java script class, and so returning a class's attribute is just returning some javascript data.

![[Screenshot 2026-06-21 at 10.33.04 AM.png|500]]

On top of that, we can also add a state to this component, like whether if we liked the comment or not.

![[Screenshot 2026-06-21 at 10.36.10 AM.png|500]]

This could easily be done with the addition of a little list (did we like something or not), and then jus returning the state of either `liked` or `like`.

![[Screenshot 2026-06-21 at 10.49.15 AM.png|500]]

---
## Wrap Up Example

So, recalling from the example from the beginning of the class, how would someone make this facebook-like page?

![[Screenshot 2026-06-21 at 11.26.56 AM.png|500]]

Well... it looks like a lot at first, but when we break it down into it's components, it's not as difficult as it seems.

![[Screenshot 2026-06-21 at 11.27.20 AM.png|500]]


First is the `<App />` component, as we see, it's just made up of `<NavBar />`, `<Intro />`, `<Photos />`, `<Post />`.

![[Screenshot 2026-06-21 at 11.29.49 AM.png|500]]


Starting from `<Intro />`, it has a `studies at xxx` text, and a `from xxx` text, we can get those values from props.

![[Screenshot 2026-06-21 at 12.29.05 PM.png|500]]


As for `<Photos />`, we can have a map function that maps images into a jsx format of `<img/>`.

![[Screenshot 2026-06-21 at 12.30.48 PM.png|500]]


Next is `<Post />`, this is pretty standard to what we had so far, nothing new.

![[Screenshot 2026-06-21 at 12.32.28 PM.png|500]]


And then we have this `state` of liking the post or not, to trigger about re-rendering.

![[Screenshot 2026-06-21 at 12.33.26 PM.png|500]]


So... frontend isn't that crazy! React helped us organize the entire thing mentally a lot.