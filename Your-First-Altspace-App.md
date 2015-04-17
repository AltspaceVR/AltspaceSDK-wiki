This tutorial takes you from checking out the SDK on GitHub to creating a simple app.  When run in the [[Altspace Web Browser]], this app imports an object loaded from a 3D model file into the Altspace virtual reality environment. The final source code listing, which is **only 30 lines of code** is shown at the end of this page.

First clone or [download] the [AltspaceSDK Repo] from GitHub.

You can also using a GitHub GUI, command line shown here for brevity.
```
$ git clone git@github.com:AltspaceVR/AltspaceSDK.git
```
This will create the AltspaceSDK directory, with the following files and directories.
```
$ ls AltspaceSDK
src/
lib/
examples/
README.md
README.html
```
You could start building your app in this AltspaceSDK directory.  However, we recommend you **copy the SDK files into another directory** referenced by your app.  This will make your app more self-contained, and allow you to `git pull` changes from the AltspaceSDK repo without affecting your app.  Keep in mind this SDK is in BETA status and could change frequently, including non-backwards-compatible upgrades or discontinuing support for older versions.

For example, we create a MyFirstApp directory and copy SDK files as follows.
```
$ mkdir MyFirstApp
$ cp -r AltspaceSDK/src MyFirstApp/sdk
$ cp -r AltspaceSDK/lib MyFirstApp/lib
$ ls MyFirstApp/
lib/
sdk/
```
(If you use another directory structure, remember to adjust the paths used in your `<script>` tags below.)

Next, create an HTML file with script import tags pointing to the SDK files you copied above.  
```
<!DOCTYPE html>
<html lang="en">
<head>
    <title>My First Altspace App</title>
    <script src="lib/three.min.js"></script>
    <script src="lib/OBJMTLLoader.js"></script>
    <script src="lib/MTLLoader.js"></script>
    <script src="sdk/AltOBJMTLLoader.js"></script>
    <script src="sdk/AltRenderer.js"></script>
</head>
<body>
</body>
</html>
```
You can name the above file index.html, MyFirstApp.html, or whatever you like. The SDK does not require any particular directory structure or file naming.

Below we use the canonical example of importing a cube model, which you can copy from the AltspaceSDK repo `examples` directory. 
```
$ mkdir MyFirstApp/models
$ cp AltspaceSDK/examples/spinning_cube/cube.obj MyFirstApp/models/
$ cp AltspaceSDK/examples/spinning_cube/cube.mtl MyFirstApp/models/
$ cp AltspaceSDK/examples/spinning_cube/altspace-logo.jpg MyFirstApp/models/
$ ls MyFirstApp/models/
altspace-logo.jpg
cube.mtl
cube.obj
```
You can also create a model with a 3D Modeling program, or download one from any of the online catalogs (listed on the [[Resources]] page).  Be sure your model is in OBJ/MTL format, where the .obj files describes the geometry and the .mtl describes the materials of the object, as this is the only 3D object format currently supported by Altspace.  

To load your object, use the AltOBJMTLLoader available in the SDK.  Add the following code in the `<body>` section.
```
<script>
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
</script>
```
Note that we created the THREE.Scene as in a typical Three.js app.  We did not create a THREE.Camera, because apps use the exisiting Altspace first-person camera (which moves as the user moves around the virtual environment).  Another difference is instead of using a THREE.WebGLRenderer, we use the THREE.AltRenderer, discussed in the next step.  Inside the loader callback, we set the initial scale and position of the object, add it to the scene, and finally kick off the animation loop.

Now that the cube model is loaded, let's display it in Altsapce! Add this before the `</script>` tag.
```
function animate() {
	window.requestAnimationFrame( animate );
	renderer.render( scene );
};
```
You're done!  Now fire up your local web server (we recommend Prepros; see the [[Workflow]] page for more recommended development tools) to host this page and copy the URL. Then enter AltspaceVR (try it first with your HMD unplugged so Altspace runs in non-VR mode), and go to a space that has an area designated for running apps.  Open the Altspace Web Browser, copy your app URL into the address bar, and select the "beam" icon. You should now see the cube (or whatever model you chose).  If you don't, check out the [[Troubleshooting]] page. If it worked, quit Altspace, plug in your Oculus Rift DK2, and view your app running in VR.  

Congratulations, you created your first Altspace Web App!

```
<!DOCTYPE html>
<html lang="en">
<head>
    <title>My First Altspace App</title>
    <script src="lib/three.min.js"></script>
    <script src="lib/OBJMTLLoader.js"></script>
    <script src="lib/MTLLoader.js"></script>
    <script src="sdk/AltOBJMTLLoader.js"></script>
    <script src="sdk/AltRenderer.js"></script>
</head>
<body>
<script>
var scene = new THREE.Scene();
var renderer = new THREE.AltRenderer();
var cube;
var loader = new THREE.AltOBJMTLLoader();
loader.load("models/cube.obj", function ( loadedObject ) {
	cube = loadedObject;
	cube.scale.set( 2, 2, 2);
	cube.position.y = 25;
	scene.add( cube );
	animate();
});
function animate() {
	window.requestAnimationFrame( animate );
	renderer.render( scene );
};
</script>
</body>
</html>
```

[AltspaceSDK Repo]: https://github.com/AltspaceVR/AltspaceSDK
[README]: https://github.com/AltspaceVR/AltspaceSDK
[download]: https://github.com/AltspaceVR/AltspaceSDK/archive/master.zip
[Three.js Examples]: http://threejs.org/examples/

