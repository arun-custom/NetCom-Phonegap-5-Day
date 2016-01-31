# Phonegap Continued

## Geolocation
- The Geolocation API allows us to access the device's geolocation features such as the GPS and cell triangulation features.
- Let's take a look at the documentation [here](http://plugins.cordova.io/#/package/org.apache.cordova.geolocation).
- In order to use this feature we have to install the plugin:

```
cordova plugin add org.apache.cordova.geolocation
```

- This plugin also adds to the global `navigator` object to contain its methods.
- Let's take a look at the `getCurrentPosition` method:

```javascript
navigator.geolocation.getCurrentPosition(onSuccess, onError, options);

function onSuccess(position) {
	alert("Latitude: " + position.coords.latitude);
	alert("Longitude: " + position.coords.longitude);
}

function onError(error) {
	alert("Error Code: " + error.code);
}
```

- The options object also gives us control over a few key aspects:
	- enableHighAccuracy: Tells the application to give the best results when possible.
	- timeOut: Maximum time allotted between call to the `navigator` function and the success handler.
	- maximumAge: Accept cached position based on age of the result.

## In-Class Lab: Mapping
- In this lab we will be taking the latitude and longitude coordinates from the device and rendering a Google Map.
- For the Google Map you will need to use the Google Maps JavaScript API located [here](https://developers.google.com/maps/documentation/javascript/tutorial).
- Your mission is to give the user a button they can click on that will render a map of their current location.

## oAuth with Phonegap
- oAuth with Phonegap can be done in one of two ways: the JavaScript approach or the native approach.
- In the JavaScript method, we must send the user over to the login page via an in-app browser.
- Via the native method we can use a plugin to handle the login via the native app on the device.

## Facebook Login
- We will learn how to perform Facebook login with this plugin: https://github.com/Wizcorp/phonegap-facebook-plugin.
- This plugin uses Objective-C to perform the native login, which is activated by the JavaScript code we write.

## Using Local Databases with Phonegap
- Phonegap doesn't come with a pre-installed database.
- There are two main options for persisting data in Phonegap: HTML5 localStorage and SQLite.
- localStorage is great for storing small amounts of data, but when you need a more robust solution you should use SQLite.
- SQLite is a plugin and can be found here: https://github.com/litehelpers/Cordova-sqlite-storage.
- Here is how we could use it to persist data:

Open the database:

```javascript
var db = window.sqlitePlugin.openDatabase({name: "my.db"});
```

Execute SQL:

```javascript
db.executeSql("SELECT * FROM todos", [], function (res) {
	console.log('got stringlength: ' + res.rows.item(0).stringlength);
}, function(error) {
	console.log('SELECT error: ' + error.message);
});
```

## Todo List Lab
- In this lab we will be creating a todo list app with jQuery Mobile and SQLite.
- Your task is to set up a simple UI with jQuery Mobile and to save your todos with SQLite.