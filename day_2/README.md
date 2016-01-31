# Introduction to jQuery Mobile

## Running jQuery Mobile Apps
- Since apps built in jQuery Mobile use AJAX to swap pages in and out, you will need to run your application from a web server.
- The easiest way to do this is with the Python SimpleHTTPServer that comes with the Mac Developer Tools:

```
python -m SimpleHTTPServer 3000
```

## What is jQuery Mobile?
- Mobile framework that uses jQuery
- Cross-browser, cross-platform tool
- Platform to create app front end that looks native
- Markup-driven, minimal code needed
- Documentation can be found [here](http://jquerymobile.com/).

## How jQuery Mobile Works
- Elements are given custom attributes to attach specific functionality.
- Each "page" of the app has its own div with a "data-role" attribute with a value of "page."
- CSS classes are added automatically by the framework to create style.
- Components such as form elements and lists are enhanced by the framework.
- "Pages" are swapped in and out of view by JavaScript.
- jQuery Mobile is for the UI. Any native functionality such as camera, accelerometer, GPS, etc is handled by Phonegap.

Page template:

```html
<div data-role="page" id="index">
	<div data-role="header">
    </div>
    <div data-role="content">
    </div>
    <div data-role="footer">
    </div>
</div>
```

## jQuery Mobile Events
- Events allow us to attach functionality to our applications that only trigger when those events are received.
- In addition to the standard jQuery events, we also have a number of jQuery Mobile-specific events:
- Page events:
	- pageshow
	- pagecreate
	- pageload
- Touch events:
	- tap
	- swipe
	- taphold

## Kitchen Sink Demonstration
- In this demonstration we will be looking at a few common components that are built into the jQuery Mobile Framework.
- We will be implementing these components:
	- Navbar
	- Buttons
	- Link list with filter
	- Toolbar
	- Form input
	- Range slider
	- Flipswitch
	- Select list
	- Check list with filter

## Wine Manager Lab
- In this lab we will be utilizing the components we learned to build a wine manager system.
- You will need to create a "Wine API" instance on MyAPI.
- We will be building 4 pages - show all wines, show one wine, add wine, edit wine.