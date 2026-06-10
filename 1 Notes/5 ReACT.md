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

---

https://www.youtube.com/watch?v=wIyHSOugGGw
