This tutorial takes you from checking out the SDK on GitHub to creating a simple app.  

When run in the [[Altspace Web Browser]], this app imports an object loaded from a 3D model file into the Altspace virtual reality environment. The final source code listing, which is **only 23 lines long** is shown at the end of this page.

First clone or [download] the [AltspaceSDK Repo] from GitHub.
```sh
$ git clone git@github.com:AltspaceVR/AltspaceSDK.git
```
This will create the AltspaceSDK directory, with the following files and directories.
```sh
$ ls AltspaceSDK
src/
lib/
examples/
README.md
README.html
```
You could start building your app in this AltspaceSDK directory.  However, we recommend you **copy the SDK files into another directory** referenced by your app.  This will make your app more self-contained, and allows you to `git pull` updates from the AltspaceSDK repo without affecting the files used by your app.

For example, we create a MyFirstApp directory and copy SDK files as follows.
```sh
$ mkdir MyFirstApp
$ cp -r AltspaceSDK/src MyFirstApp/sdk
$ cp -r AltspaceSDK/lib MyFirstApp/lib
$ ls MyFirstApp/
lib/
sdk/
```
(If you use another directory structure, adjust the paths used in `<script>` tags below.)

Next, create an HTML file with script import tags pointing to the SDK files.  
```html
<!DOCTYPE html>
<html lang="en"> <head>
    <title>My First Altspace App</title>
    <script src="lib/three.min.js"></script>
    <script src="lib/OBJMTLLoader.js"></script>
    <script src="lib/MTLLoader.js"></script>
    <script src="sdk/AltOBJMTLLoader.js"></script>
    <script src="sdk/AltRenderer.js"></script>
</head> <body> <script>
</script> </body> </html>
```
You can name the above file index.html, MyFirstApp.html, or whatever you like. The SDK does not require any particular directory structure or file naming.

Below we use a cube model, available in the AltspaceSDK repo `examples` directory. 
```sh
$ mkdir MyFirstApp/models
$ cp AltspaceSDK/examples/models/AltspaceCube/cube.obj MyFirstApp/models/
$ cp AltspaceSDK/examples/models/AltspaceCube/cube.mtl MyFirstApp/models/
$ cp AltspaceSDK/examples/models/AltspaceCube/altspace-logo.jpg MyFirstApp/models/
$ ls MyFirstApp/models/
altspace-logo.jpg
cube.mtl
cube.obj
```
You can also create a model with a 3D Modeling program, or download one from any of the online catalogs (listed on the [[Resources]] page).  Be sure your model is in OBJ/MTL format, where the .obj files describes the geometry and the .mtl describes the materials of the object, as this is the only 3D object format currently supported by Altspace.  

Now let's load the model.  Add the following code after the `<script>` tag.
```js
var scene = new THREE.Scene();
var renderer = new THREE.AltRenderer();
var cube;
var loader = new THREE.AltOBJMTLLoader();
loader.load("models/cube.obj", function ( loadedObject ) {
	cube.scale.set( 2, 2, 2);
	cube.position.y = 25;
	scene.add( cube );
	animate();
});
```
We created the THREE.Scene as in a typical Three.js app.  We did not create a THREE.Camera, since apps use the exisiting Altspace first-person camera.  Another difference is instead of using the standard WebGLRenderer and OBJMTLLoader, we use the SDK AltOBJMTLLoader and AltRenderer.  Inside the loader callback, we set the initial scale and position of the object, add it to the scene, and kick off the animation loop.

Now let's render the object in Altsapce. Add this before the `</script>` tag.
```js
function animate() {
	window.requestAnimationFrame( animate );
	renderer.render( scene );
};
```
Now fire up your local web server (we recommend Prepros; see the [[Workflow]] page) to host this page, then copy the URL. Enter AltspaceVR (try it first with your HMD unplugged, non-VR mode), and go to a space that has an area designated for running apps.  Open the Altspace Web Browser, copy your app URL into the address bar, and select the "beam" icon. You should now see the cube or whatever model you chose.  If you don't, see the [[Troubleshooting]] page. If it worked, quit Altspace, plug in your Oculus Rift DK2, and repeat to view your app running in VR.  

Congratulations, you created your first Altspace Web App!

```html
<!DOCTYPE html>
<html lang="en"> <head>
    <title>My First App</title>
    <script src="lib/three.min.js"></script>
    <script src="lib/OBJMTLLoader.js"></script>
    <script src="lib/MTLLoader.js"></script>
    <script src="sdk/AltOBJMTLLoader.js"></script>
    <script src="sdk/AltRenderer.js"></script>
</head> <body> <script>
var scene = new THREE.Scene();
var renderer = new THREE.AltRenderer();
var loader = new THREE.AltOBJMTLLoader();
loader.load("models/cube.obj", function ( object ) {
	object.scale.set( 2, 2, 2);
	object.position.y = 25;
	scene.add( object );
	animate();
});
function animate() {
	window.requestAnimationFrame( animate );
	renderer.render( scene );
};
</script> </body> </html>
```

[AltspaceSDK Repo]: https://github.com/AltspaceVR/AltspaceSDK
[README]: https://github.com/AltspaceVR/AltspaceSDK
[download]: https://github.com/AltspaceVR/AltspaceSDK/archive/master.zip
[Three.js Examples]: http://threejs.org/examples/
