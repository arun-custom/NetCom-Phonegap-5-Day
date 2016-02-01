# Introduction to Phonegap / Cordova

## What is Phonegap / Cordova?
- Cordova is an API that allows you to write JavaScript commands that map over to native device commands.
- Phonegap is a distribution of Cordova, and also wraps in functionality such as its build tools.

## Installation

#### Build Tools
- For this class we will need to have Xcode installed with the latest command line and build tools:

```
xcode-select --install
```

- You will also need the Android SDK. You can find it [here](http:
- For compiling Android apps you will need to download and install Apache Ant.
	- Windows [click here](http://ant.apache.org/bindownload.cgi)
	- With Mac it can be installed easily with Homebrew: `brew install ant`.

#### Command Line Tools
- You will need to have Cordova and the Cordova-Cli installed, as well as the latest version of Phonegap:

```
sudo npm install cordova -g
sudo npm install phonegap -g
```

## Creating a New Project
- To create a new project we can run the `cordova create` command:

```
cordova create hello com.example.hello HelloWorld
```

- The first parameter is the folder you want to generate. The second is a reverse domain identifier, and the third is the name of the project.
- When you run this command you will see a number of folders generated for you:
	- Platforms: This folder holds information and native code for each platform you choose to target such as Android or iOS.
	- Plugins: This folder will hold all of the plugin-related code that comes in importing the plugin via the command line.
	- Www: This folder will contain all of your HTML, CSS and JavaScript project files. Eventually it will be added to each platform's appropriate folder to be included in the main app.

## Cordova.js
- In order to run any native commands via JavaScript you have to include cordova.js in your project.
- This file will not exist in your `www` directory but will be included upon build.
- Make sure to include a link to the file in your main HTML document:

```html
<script src="cordova.js"></script>
```

## Cordova Plugins
- Plugins are the modules of code that allow you to write JS commands that trigger native actions.
- Most of the major native functionality is wrapped into various plugins, such as accessing the camera or pulling from the GPS.
- Let's take a look at the plugin registry to see what's available to use. It can be found [here](http://cordova.apache.org/docs/en/4.0.0/cordova_plugins_pluginapis.md.html).

## Building Your App
- Building the app is pretty trivial if you have all of the utilities set up.
- There are a couple of command line tools to help us with this:

```
cordova build ios
cordova build android
```

- Building for iOS will use Xcode's compiler to compile the app whereas building for Android will trigger Ant for compilation.
- If the build succeeds you should be able to now emulate the app:

```
cordova emulate ios
cordova emulate android
```

- This will attempt to open the default emulator for the build type. This works well on Android but requires additional software for iOS.
- It is recommended to work through Xcode when running and debugging iOS apps.

## Emulating Your App
- Using your new app on your actual device is an important testing step.
- We will download the Phonegap Developer app from the iTunes store to display the app on our device.

## deviceready
- It is important to note that all of the Cordova plugins require the device to be ready before they can be accessed.
- Cordova provides us an event called `deviceready` that signals to our application that we can safely call Cordova commands.
- The syntax is exactly the same as any other event listener:

```javascript
document.addEventListener("deviceready", function() {
	//Device is ready and you can use Cordova
});
```

## Using the Device Camera
- Let's take a look at the documentation [here](http://plugins.cordova.io/#/package/org.apache.cordova.camera).
- We need to first use the Cli to install the plugin:

```
cordova plugin add org.apache.cordova.camera
```

- This plugin adds an object to the `navigator` global object called `camera` that has methods associated with it:

```javascript
navigator.camera.getPicture(cameraSuccess, cameraError, cameraOptions);
```

- Here is an example from the documentation with an option and all appropriate callbacks:

```javascript
navigator.camera.getPicture(onSuccess, onFail, {
	quality: 50,
	destinationType: Camera.DestinationType.FILE_URI 
});

function onSuccess(imageURI) {
	var image = document.getElementById('myImage');
	image.src = imageURI;
}

function onFail(message) {
	alert('Failed because: ' + message);
}
```

- There are a number of options you can set to customize the camera action to your needs:

```javascript
{ 
	quality : 75,
	destinationType : Camera.DestinationType.DATA_URL,
	sourceType : Camera.PictureSourceType.CAMERA,
	allowEdit : true,
	encodingType: Camera.EncodingType.JPEG,
	targetWidth: 100,
	targetHeight: 100,
	popoverOptions: CameraPopoverOptions,
	saveToPhotoAlbum: false
}
```

- Specifically important are the options `Camera.DestinationType.[option]`, which can save the picture as a binary file or a Base64 encoded string, and `Camera.PictureSourceType.[option]`, which can either take a new picture or select one from the camera roll.

## In-Class Exercise: The Social Network
- We will be creating a user manager app in class that will utilize a few Cordova APIs.
- The front end has already been completed for you [here](social_network_starter_app/).
- Your job is to activate the functionality using the MyAPI Members endpoint.
- Here are the API endpoints you will need:
	- `GET /members` -> Retrieve all members
	- `GET /members/:id` -> Get one member
	- `POST /members` -> Create a new member
	- `PUT /members/:id` -> Update a member
	- `DELETE /members/:id` -> Delete a member
- **Bonus:** Implement different jQuery Mobile transitions to smoothly navigate between pages.

## FileTransfer API
- The FileTransfer API allows you to upload and download files using the native device.
- This is especially useful for allowing users to upload photos from their device.
- Let's take a look at the documentation [here](http://plugins.cordova.io/#/package/org.apache.cordova.file-transfer).
- Here is our install command:

```
cordova plugin add org.apache.cordova.file-transfer
```

- This plugin offers a new constructor function `FileTransfer` that gives you methods for uploading and downloading the files.
- To use the plugin we have to create an instance of the constructor:

```javascript
var ft = new FileTransfer();
```

- You will likely need to set a number of options to configure your file transfer:

```javascript
var options = {
	fileKey: "file",
	fileName: "sample",
	params: { },
	mimeType: "image/jpeg"
};
```

- We can then call on the file transfer functions such as upload:

```javascript
ft.upload(fileURL, encodeURI("url here"), success, error, options);
```

## FileTransfer Exercise: Photo Upload
- Let's take the social network app we just created and add a file transfer component to it.
- When a user takes or selects a photo let's use the FileTransfer API to send the file to the server.
- Make sure to submit this request on success of the add user method so you can pass along the user id.
- Here is the endpoint you will need to access:
	- `POST /members/:id/photo` -> Upload a profile photo for a member
- **Bonus:** Check out the `onprogress` event that is triggered throughout the transfer. Try to implement a simple progress bar that updates with the status of the upload.

## Accessing Device Contacts
- This API can be useful for adding contacts on behalf of users and also accessing the contact list for use in the app.
- Let's take a look at the documentation [here](http://plugins.cordova.io/#/package/org.apache.cordova.contacts).
- The contacts API appends to the `navigator` global object to apply its methods.
- The first method we will look at is the `create()` function that creates a new contact:

```javascript
var myContact = navigator.contacts.create({"displayName": "Test User"});
```

- Try it by yourself to add a contact with a few additional fields.

## Contacts Exercise: Add to Contacts
- Let's take the social network and add a contacts component to it.
- After the AJAX save and file upload try to add the contact to the contact database on the device.
- **Bonus:** Check to see if the contact exists already on the device before saving it.