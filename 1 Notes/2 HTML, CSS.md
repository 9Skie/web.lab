There was this really funny description of what these three languages are for web dev:

![[Pasted image 20260609145913.png|400]]

HTML is the skeleton, CSS is the skin, and JavaScript is the brain.

Think of it this way: **HTML** structures the page's content, **CSS** makes it visually appealing, and **JavaScript** brings it to life with interactivity.

Right now, we'll start by looking at HTML, it defines 'where' things are on a page, for the most part.

Let's take a look at xkcd comic's home page:

![[Screenshot 2026-06-09 at 3.15.35 PM.png|300]]

Underneath, it's all defined by these 'boxes' of HTML of where things are laid out on a page.

![[Screenshot 2026-06-09 at 3.17.00 PM.png|300]]

So, what is HTML? Fundamentally, HTML at its simplest glance looks something like this:

![[Screenshot 2026-06-09 at 3.17.52 PM.png|300]]

It's not very exciting... we just have a dull heading and a paragraph

![[Screenshot 2026-06-09 at 3.23.44 PM.png|500]]

- The `<!DOCTYPE html>` declaration defines that this document is an HTML5 document
- The `<html>` element is the root element of an HTML page
- The `<head>` element contains meta information about the HTML page

- The `<title>` element specifies a title for the HTML page (which is shown in the browser's title bar or in the page's tab)
	- ![[Screenshot 2026-06-09 at 3.27.54 PM.png|400]]

- The `<body>` element defines the document's body, and is a container for all the visible contents, such as headings, paragraphs, images, hyperlinks, tables, lists, etc.
	- ![[Screenshot 2026-06-09 at 3.28.04 PM.png|400]]

- The `<h1>` element defines a large heading
	- ![[Screenshot 2026-06-09 at 3.28.27 PM.png|400]]

- The `<p>` element defines a paragraph
	- ![[Screenshot 2026-06-09 at 3.28.37 PM.png|400]]

While, yeah, that's a lot to take in... these are all HTML elements, an HTML element is defined by a start tag, some content, and an end tag:

![[Screenshot 2026-06-09 at 3.19.15 PM.png|400]]

So, as we see above, some tags are on one line (like `<p>`), and some tags are on many lines (like `<body>`). The HTML element is everything from the start tag to the end tag, so beware what wraps around what.

![[Screenshot 2026-06-09 at 3.20.32 PM.png|300]]

In our very minimalistic example, we can already see a lot of tags flying around the screen, tags act like containers inside containers, and you'll quickly see structures several levels deep.

![[Screenshot 2026-06-09 at 3.21.28 PM.png|300]]

For certain tags, there are additional attributes that you can add to the tag.

![[Screenshot 2026-06-09 at 4.09.15 PM.png|300]]

- Like inserting a link to click.
	- ![[Screenshot 2026-06-09 at 4.08.50 PM.png|300]]

- Or inserting an image
	- ![[26C00157-009C-4397-9713-2D4355EBC6A3.png|300]]
	- The source file (`src`), alternative text (`alt`), `width`, and `height` are provided as attributes.

We can learn 2 interesting thing from the image tag.
- not all tags need a open and a close, the `img` tag is self closing
	- ![[Screenshot 2026-06-09 at 4.18.30 PM.png|300]]
- the source of images could be remote/local
	- ![[Screenshot 2026-06-09 at 4.19.17 PM.png|300]]

The most generic tags you can have is `<div>` and `<span>`
 - div is grouping a block section of a document
 - span is grouping a block section too, inline

![[Screenshot 2026-06-09 at 4.26.01 PM.png|400]]

Now, I'll stop here for HTML. There's a lot of breadth to it — tons of different tags for different functionalities — but until you actually need a specific feature, you'll likely discover the right tag exists when the time comes. There's no point in remembering random tags ahead of time for no use.

![[Screenshot 2026-06-09 at 4.22.37 PM.png|500]]

---
## CSS

CSS (Cascading Style Sheets) is the language we use to style a Web page.
- CSS describes how HTML elements are to be displayed on screen, paper, or in other media
- CSS saves a lot of work. It can control the layout of multiple web pages all at once

In general, CSS looks like this:

![[Screenshot 2026-06-09 at 4.34.02 PM.png|500]]

CSS is used to define styles for your web pages, including the design, layout and variations in display for different devices and screen sizes.

Without CSS, our HTML page looks something like this:

![[Screenshot 2026-06-09 at 4.36.58 PM.png|500]]

With CSS, our HTML page looks like this:

![[Screenshot 2026-06-09 at 4.37.38 PM.png|500]]

Here's what that CSS did to the page:
- `color: red;` - changed the text color inside the div to red
- `font-family: Arial;` - changed the font to Arial
- `font-size: 24pt;` - made the text 24 points, roughly double the default size

If you see, it only changed those visuals for things inside the `<div>`, as we see it was only selected for the div, every div will be affected by this css visual change,

Hm... but what if we don't want those changes to all divs? What if we wanted it to be more specialized? We can do that too, through ids.

1. we add a class to the tag that we want to have the visual, (in this case named `info`)
	- ![[Screenshot 2026-06-09 at 4.51.23 PM.png|400]]
2. we change our css selector to be for that class `info`
	- ![[Screenshot 2026-06-09 at 4.52.12 PM.png|400]]


Another way to do it is through a `id`.

![[Screenshot 2026-06-09 at 5.00.57 PM.png|500]]


Visually, it seems that nothing has changed, id seems to have the exact same effect as class, then what's the point of id?

|                  | **class**                                               | **id**                                                        |
| ---------------- | ------------------------------------------------------- | ------------------------------------------------------------- |
| **Used on**      | Multiple elements (same class on many tags)             | Only one element per page (each id must be unique)            |
| **CSS selector** | `.classname` (starts with a dot)                        | `#idname` (starts with a hash)                                |
| **HTML example** | `<div class="info">`                                    | `<div id="main-header">`                                      |
| **When to use**  | Styling groups of things (cards, buttons, paragraphs)   | Targeting a single element (a specific section, a form field) |

A single tag can have multiple classes, just separate them with spaces: `<div class="info highlight">`. This lets you mix and match styles (one class for color, another for layout) without rewriting CSS.


But we come to a new problem, which comes out on top? If we have a div selector that makes the color of the text red, then a div has a class which makes the color blue, and another in the same div that makes the color green, and it has an id that makes it yellow... who comes on top?

There is built in heirchy in CSS:

1. IDs come out on top
2. then we have classes
3. last comes general element selectors

![[Screenshot 2026-06-09 at 5.07.36 PM.png|400]]

Usually people just use class 1 + class 2 + class 3... etc, IDs and element selectors are rarely used.




