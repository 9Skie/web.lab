A new day, a new workshop! End of this workshop our page should look like this:

![[Screenshot 2026-07-15 at 10.52.21 AM.jpg|500]]

Not... very... different from before? Yeah, not very different, we jus want everything to visually fall under React through a component tree, instead of raw HTML.

![[Screenshot 2026-07-15 at 11.01.12 AM.jpg|500]]

The code has uh... already put components divided in this state, take a look:

![[Screenshot 2026-07-15 at 11.07.47 AM.jpg|500]]

The design philosophy for this type of arrangement is one file per component. It's the React convention: each UI piece (navbar, profile, cat happiness box) gets its own file so its code is isolated and reusable.
- `App.js` : root, just assembles the pieces
- `pages/` : whole screens (Profile)
- `modules/` : reusable widgets (NavBar, CatHappiness) that any page could use

---
## Exercise 1

Make a Navbar...

Bro I thought this was gonna be so hard ahhh I never worked with React before and you are telling me it basically looks like returning HTML, bruh.

```jsx
const NavBar = () => {
  return (
    <nav className="NavContainer">
      <div class="navTitle">Catbook</div>
    </nav>
  );
};
```

---
## Exercise 2

Give the navbar it's colors and spacing stuff...

We can just copy this over from the previous workshop, there's no need to re-invent new colors and stuff.

The root is from another file, `utilities.css` which is given to us, I just copied the toor down here for visibility.

```css
:root { 
     --primary: #396dff;
     --grey: #f7f7f7;
     --white: #fff;
     --xs: 4px;
     --s: 8px;
     --m: 16px;
     --l: 24px;
 } 

 .NavContainer {
    padding: var(--s) var(--m);
    background-color: var(--primary);
 }
```

---
## Exercise 3

Now... cat happiness... that box that contains the number of clicks of when we click on the profile picture.

How????? Man!!!!!

![[Screenshot 2026-07-15 at 11.56.44 AM.jpg|500]]

It's just 'where' things are placed are so annoying to me in frontend, dude, anyways.

The first part of adding the state is going to `Profile.js`, and adding this 1 single line:

```jsx
const [catHappiness, setCatHappiness] = useState(0);
```

Which adds that as the initial value for cat happiness.


And to import cat happiness into `Profile.js`, it's just as simple as 1 line as well:

```jsx
import CatHappiness from "../modules/CatHappiness";
```

How annoying is this... javascript...

Then we inserted `<CatHappiness />` into the page by using this line into `Profile.jsx`:

```jsx
<CatHappiness catHappiness={catHappiness} />
```

---
## Exercise 4

Now, we want to make it such that we click the button of the profile picture, it increments the counter.

So we write a function:

```jsx
const incrementCatHappiness = () => {
	setCatHappiness(catHappiness + 1);
};
```

And then we just need this function to happen under in the returned display:

```jsx
<div className="Profile-avatar u-pointer" onClick={incrementCatHappiness} />
```

