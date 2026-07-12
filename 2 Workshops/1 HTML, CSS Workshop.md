The goal of workshop 1 (or as they like to call it, 0) is to make the page look something like this:

![[Screenshot 2026-07-08 at 4.11.13 PM.png|500]]

Looks like just a bunch of HTML & CSS play! Let's go.

---
## Exercise 1:

Try to copy something like this:

![[Screenshot 2026-07-08 at 4.20.12 PM.png|500]]

My answer:

```html
<!DOCTYPE html>
<html>
	<head>
		<title>Catbook</title>
	</head>

	<body>
		<h1>Buka Buka</h1>
		<hr>

		<b><p>About Me</p></b>
		<p>I am more of a turtle person but I'm just trying to fit in and get a catbook</p>

		<b><p>My Favorite Type of Cat</p></b>
		<p>I actually prefer turtles</p>
	</body>
</html>
```

- The dude added a `<section>` header in between... that's whatever

---
## Exercise 2

All we did was just add one line `<img src="cat.png">`, it's just adding an image.

![[Screenshot 2026-07-08 at 4.40.52 PM.png|500]]

---
## Exercise 3

This was interesting! So basically, we can place classes on top of sections, and we have to do link to stylesheets.

![[Screenshot 2026-07-08 at 4.59.55 PM.png|500]]

This is the CSS file, named `styles.css`, which we added to the HTML

```css
.u-textCenter {
	text-align: center;
}
```

---
## Exercise 4

Now we downloaded a font from [google](https://fonts.google.com/), personally I liked the pixel-ish looking font so I downloaded it, and added it to the css file.

```css
.geist-pixel {
  font-family: "Geist Pixel", sans-serif;
  font-optical-sizing: auto;
  font-weight: 400;
  font-style: normal;
  font-variation-settings:
    "ELSH" 0;
}
```

Then we edited the HTML file.

```html
<!DOCTYPE html>
<html>
	<head>
		<title>Catbook</title>
		<link rel="preconnect" href="https://fonts.googleapis.com" />
		<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
		<link href="https://fonts.googleapis.com/css2?family=Geist+Pixel&display=swap" rel="stylesheet" />
		<link rel="stylesheet" href="styles.css" />
	</head>

	<body>
		<img src="cat.png" alt="turtle" />
		<h1 class="u-textCenter geist-pixel">Buka Buka</h1>
		<hr />

		<section class="u-textCenter geist-pixel">
			<h4>About Me</h4>
			<p>
				I am more of a turtle person but I'm just trying to fit in and get a catbook.
			</p>
		</section>

		<section class="u-textCenter geist-pixel">
			<h4>My Favorite Type of Cat</h4>
			<p>I actually prefer turtles.</p>
		</section>
	</body>
</html>
```

---
## Exercise 5

We are now adding a navbar, which is just this little simple guy in HTML:

```html
<nav class="navContainer">
	<h1 class="navTitle">Catbook</h1>
</nav>
```

It needs a class of styling called navTitle, so... we made that as well.

```css
:root {
	--primary: #396dff;
	--grey: #ffffff;
	--white: #ffffff;
}

.navTitle {
	color: var(--primary);
	font-size: 20px;
}
```

---
## Exercise 6

Now we are trying to make the navbar to have some style? 

![[Screenshot 2026-07-12 at 8.48.42 AM.png|500]]

Well, to make the background blue, we just make another css class:

```css
.navContainter {
    background-color: var(--white);
}
```

---
## Exercise 7

However... there's this white margin on the side of the screen, how do we remove that?

![[Screenshot 2026-07-12 at 8.55.26 AM.png|500]]

Well, welcome to annoying CSS, it's how we define content, padding, boarder, and margins.

CSS content is the element itself, padding is space inside it, a border wraps it, and margin is space outside it.

![[Pasted image 20260712090230.png|500]]

So we are needing to deliberately set that margin to 0, which right now it's set to 8 for some reason by default.

![[Screenshot 2026-07-12 at 9.07.10 AM.png|500]]

One way that we could do it is just set `margin: 0 0 0 0;` and that works, but another idea is the '8pt Grid System', it's a design rule where spacing and sizing use multiples of 8 pixels to keep layouts consistent.

So we will follow that as well, and we won't have to directly say 8px 16px explicitly, we can just use those pre-set values (variables) for how we want certain things to align.

```css
:root {
  --primary: #396dff;
  --grey: #ffffff;
  --white: #ffffff;

  --none: 0px;
  --xs: 4px;
  --s: 8px;
  --m: 16px;
  --l: 24px;
}

body {
  font-family: "Open Sans", sans-serif;
  margin: var(--none);
}

```

---
## Exercise 8/9

Uhhh I don't care about rounded corners so I skipped that one, now the question is how to turn our square image into a circle and put it in the center.

![[Screenshot 2026-07-12 at 9.48.06 AM.png|300]]

To turn a square image into a circle, use the CSS property `border-radius: 50%`.

But... to make sure we don't stretch the image, and make sure it's center aligned... we have to add some extra things.
-  `display: block` makes the `<img>` act like a standalone box that takes its own line, so `margin: 0 auto` can actually center it.
- `object-fit: cover` makes the image keep its natural aspect ratio while filling the box, so no deformation happens.

```html
<img src="cat.png" class="circle" alt="turtle"/>
```

```css
.circle {
  width: 300px;
  height: 300px;
  border-radius: 50%;
  display: block;
  margin: 0 auto;
  object-fit: cover;
}
```

----
## Exercise 10

Now, we want to display these side by side instead of top to bottom.

![[Screenshot 2026-07-12 at 9.51.54 AM.png|500]]

This requires something called a flex box, which is like... boxes of text instead of our original alignment.

![[Screenshot 2026-07-12 at 11.36.26 AM.png|500]]

You can just make a class called flex, and then chose the flex direction to be either column or row.

![[google-docs-image.gif|500]]

So we added something like that to the CSS:

```css
.flexbox {
    display: flex;
    flex-direction: row;
    gap: var(--m);
    padding: var(--m);
}
```

---
## Exercise 11

Uh... something still looks a bit off? It's not centered to where we want.

![[Screenshot 2026-07-12 at 12.06.38 PM.png|500]]

So... we have to turn to more flex box tricks! One is called flex basis, we we can set the size of flex boxes to be different depending on our needs.

![[73fa45ed-28da-4346-ad68-81bb74c85210.gif|500]]

The other is flex grow, it's a binary that we set such that we can define what items gets to take up more space.

![[33667c41-3382-4007-82ee-b82c181098b9.gif|500]]

Well, add both of these to our current flex box...

```css
.flexbox {
    display: flex;
    flex-direction: row;
    gap: var(--m);
    padding: var(--m);
    max-width: 800px;
    margin: 0 auto;
}

.flexbox > section {
    flex-basis: 0;
    flex-grow: 1;
}
```

We get a nice looking website!

![[Screenshot 2026-07-12 at 12.12.40 PM.png|500]]