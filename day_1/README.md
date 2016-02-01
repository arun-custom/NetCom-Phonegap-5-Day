# HTML, CSS, jQuery Refresher

## CSS Positioning
- There are four main types of positioning that you will see most often - static, relative, absolute, and fixed.
- Static positioning is what all elements have by default. Yay!
- Relative and absolute work together - elements can be positioned absolutely relative to their container.
- Fixed position elements are essentially absolute relative to the window no matter where they are in the DOM. A.K.A. the window is always the relative parent.

## Positioning Exercise
- Try to replicate the following mockups using what we've talked about in this class so far.
- Utilize margins, padding, floats, positioning, etc.

1. Stackers!

![Stackers!](img/stackers.png)

2. The Mirror

![The Mirror](img/the_mirror.png)

3. The Skinny

![The Skinny](img/the_skinny.png)

4. The Absolute

![The Absolute](img/the_absolute.png)

## Floats
- Floating elements allows us to create a nearly unlimited number of layouts using all types of block elements.
- Floating an element essentially removes it from the standard "flow" and places it to the left or right side of its container.
- Elements can have fixed width, which will wrap underneath each other if the container is smaller than the combined widths.
- You can also used percentage width, which will have the columns respond to the screen size.
- You can tell already that the calculations can get out of hand really fast...

## Element Alignment
- To determine how we can align an element we have to first know what kind of element it is.
- Inline elements can be aligned as text, so with the `text-align` CSS property.
- Block elements can be aligned using the space around them - margin. A margin set to auto for both left and right will center the element in a container.

## The Grid Layout
- Most modern layouts operate on a standard 12-column grid system.
- If you break down any of the websites you know and love you will notice many variations on the 12 column grid.
- Each column in the grid can contain nested grids itself.
- If you want a larger box, you need to have a greater column offset.
- Here is a good pictorial to help you break it down:

![Grid Pictorial](img/grid.jpg)

## Code-Along: Let's Create Our Own Grid
- We will create a 2, 4, and 6 column grid.
- We will try nesting a grid inside another grid.

## CSS3 Media Queries
- Media queries allow you to apply and remove CSS styling based on the screen dimensions.
- This is important to create truly mobile-friendly layouts.
- To use it you have to specify screen resolution thresholds.
- Let's try an example where we want to show a div where the screen size is larger than 700 pixels:

HTML

```html
<div id="my-div"></div>
```

CSS

```css
@media(min-width: 700px) {
	#my-div {
		width:400px;
		height:400px;
		border:#000 1px solid;
	}
}
```

- Now where the screen size is below 700 pixels:

CSS

```css
@media(max-width: 700px) {
	#my-div {
		width:400px;
		height:400px;
		border:#000 1px solid;
	}
}
```

- You can also combine these values to select a range:

```css
@media(min-width: 700px) and (max-width: 900px) {
	#my-div {
		width:400px;
		height:400px;
		border:#000 1px solid;
	}
}
```

## What is jQuery?

jQuery is a cross-browser JavaScript library designed to simplify the client-side scripting of HTML.

It helps us out with:
- DOM traversal
- CSS manipulation through `style` attributes
- Event handling
- Animation
- And much more

## How to Use jQuery
- jQuery is available via CDN at `code.jquery.com`
- You can also download the library and serve it locally
- jQuery by itself is a library of functions. The team has also built additional tools that help us with a variety of things:
	- jQuery UI: A UI tool that adds features such as additional easings, a datepicker, modals, effects, and more.
	- jQuery Mobile: A mobile-optimized framework that allows you to create HTML5 mobile applications that look and act pretty real.

## jQuery Selectors
- The Sizzle selector engine wrapped into jQuery is a powerful tool to help us with manipulating DOM elements.
- The syntax is very similar to CSS:

```javascript
$("#myDiv > ul > li:first-child")
```

- Here the $ sign represents the jQuery library.
- Let's take a look at some of the selectors available to us [here](http://www.w3schools.com/jquery/jquery_ref_selectors.asp).

## jQuery Actions
- Actions almost always follow selectors.
- Actions are jQuery functions that perform an operation on the element(s) selected.
- The format is as follows:

```javascript
$("my-selector").action(options);
```

## DOM Manipulation
- The DOM manipulation functions in jQuery help you accomplish some pretty neat things.
- Here are a few common manipulations you will likely see:

On the fly CSS manipulations:

```javascript
$("my-selector").css("property", "value");
```

On the fly HTML manipulations:

```javascript
$("my-selector").html("New HTML inside here");
```

Altering CSS class attributes:

```javascript
$("my-selector").addClass("new class");

$("my-selector").removeClass("class");

$("my-selector").toggleClass("class");
```

## Event Handling
- Event handling is done very smoothly with jQuery.
- There are a few different ways it can be performed, each having their use cases.
- Let's say we have a button and want to attach an event:

HTML

```html
<button id="my-button">Click Me!</button>
```

jQuery

- This is what I like to call the shortcut method.
- It has the limitation of not working when the DOM element doesn't already exist (think AJAX loading in dynamic content).

```javascript
$("#my-button").click(function() { //Your code here });
```

- You can also bind events using `.on`
- This is also limited to elements that already exist, but it is a better approach.

```javascript
$("#my-button").on("click", function() { //Your code here });
```

- Lastly, you can account for dynamic elements through binding the event to the document itself.
- This also happens to be the most performant if you look at benchmark tests.

```javascript
$(document).on("click", "#my-button", function() { //Your code here });
```

- Here is a list of the most common events you are likely to see:
	- Click
	- Keyup
	- Keydown
	- Mouseenter
	- Mouseleave
	- Dblclick
	- Change

## jQuery Animations
- jQuery wraps in some neat animations that help us achieve some interested effects.
- jQuery animations work by altering the `style` attribute dynamically over a set period of time.
- These animations are great but less performant than CSS3 animations, which are hardware-accelerated.
- Here are a few common animations you will see:

Slide down (show the element):

```javascript
$("my-selector").slideDown();
```

Slide up (hide the element):

```javascript
$("my-selector").slideUp();
```

Slide toggle (back and forth):

```javascript
$("my-selector").slideToggle();
```

Fade in:

```javascript
$("my-selector").fadeIn();
```

Fade out:

```javascript
$("my-selector").fadeOut();
```

Fade toggle (back and forth):

```javascript
$("my-selector").fadeToggle();
```

- Each of these animation functions take three parameters: duration, easing, and callback function to be completed when the animation is complete.

## Custom Animations
- If none of the built-in animations suit you, jQuery also gives you a way to create your own animations.
- This function will dynamically alter the `style` attribute in the HTML document for each property you specify:

```javascript
$("my-selector").animate({
	"margin-top":"200px",
	"margin-left":"+=200px"
}, 600, "swing", function() {
	console.log("I just finished!");
});
```

## Animation Exercise: Gettysburg Address
- Download the exercise files [here](gettysburg_address/).
- Alter the stylesheet to hide the contents of the page initially. When the page is loaded, fade in the contents slowly.
- Give each paragraph a yellow background only when the mouse is over it.
- Make a click of the title (`<h2>`) and simultaneously fade it to 25 percent opacity and grow its left-hand margin to 20px. Then, when this animation is complete, fade the speech text to 50 percent opacity.
- Bonus: Make the style switcher work.
- Challenge: React to presses of the arrow keys by smoothly moving the switcher box 20 pixels in the corresponding direction. The key codes for the arrow keys are: 37 (left), 38 (up), 39 (right), and 40 (down).

## AJAX
- jQuery has a powerful AJAX feature that makes using AJAX painless and straightforward.
- There are a few shortcut methods, but here is the best-practice way that is advised:

```javascript
$.ajax({
	type: "POST, PUT, GET, or DELETE",
	url: "your endpoint here",
	success: function(data, textStatus, jqXHR) { },
	error: function(jqXHR, textStatus, errorThrown) { }
});
```

## Wine Manager API Lab
- In this lab we will be using an API located at `https://myapi.profstream.com` to build a user manager system.
- Your job is to use the user API to create a simple UI to display all of the users and a form to add a new user.