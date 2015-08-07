
Let's create an interactive, multi-player AltspaceVR Web App.  
Source: [examples/spinning-cube.html]

**Step 1**
Clone/download this repo and create your app HTML file.

Your app HTML file should contain script tags pointing to the SDK files (and HTML/CSS, if your app supports running in a tranditional browser).  Next, let's add Javascript that uses standard Three.js commands along with new functions from our SDK.  For larger apps, you could separate your Javascript into multiple JS files; the SDK does not impose any particular file or directory structure.  

**Step 2**
Open your project in AltspaceVR.

Setup [Prepros] and add your app's project directory. Click the *Live Preview* button and copy the link that opens.

Open AltspaceVR (for tips on windowed mode, see the [Workflow] page), and paste the Prepros preview link into one of the AltspaceVR browser windows.

You should now see a blank page, or any traditional HTML content you have added so far.

**Step 3**:
Load one or more OBJ/MTL models using the [AltOBJMTLLoader]
```
var cube;
var loader = new THREE.AltOBJMTLLoader();

// loader assumes .mtl file has same basename as .obj file
loader.load("models/AltspaceCube/cube.obj", function ( loadedObject ) {

	cube = loadedObject;
	scene.add( cube );
		
});
```
The object is now loaded, but it will not appear until the scene is rendered.

**Step 4**:
Render your scene using the AltspaceVR three.js renderer in your animate loop.
```
renderer = altspace.getThreeJSRenderer(); // during scene initialization
...
renderer.render( scene ); // in animation loop (via requestAnimationFrame)
```
Any objects loaded by AltOBJMTLLoader and added to the Three.js scene are now imported (a.k.a. spawned) into the AltspaceVR VR environment!  They remain there until you remove them from the scene.  Optionally, you can also create a WebGLRenderer, to use when your app is running outside of the AltspaceVR environment.

**Step 5**:
Implement your animations and app logic using [Three.js]
```
// in animate loop
cube.rotation.x += 0.01;
cube.rotation.y += 0.01;
```
The AltspaceVR ThreeJS renderer serializes key information about objects in your scene for use by the game engine (Unity 3D) rendering the AltspaceVR environment. Thus changes to the transform (position, rotation, scale) of the above cube are mirrored by the cube hologram in AltspaceVR. **Hologram** refers to the in-AltspaceVR 3D object controlled by an AltspaceVR Web App.


**Step 6a**:
Register objects for AltspaceVR events with [CursorEvents]
```
cursorEvents = new CursorEvents();

// optionally map mouse events to cursor events outside of Altspace
cursorEvents.enableMouseEvents( camera )

cursorEvents.addObject( cube );

cube.addEventListener( "cursordown", function( event ) {
	this.position.y += 2;
});

cube.addEventListener( "cursorup",  function( event ) {
	this.position.y -= 2;
});

...
// in animate loop
cursorEvents.update();
```
Now the cube will appear to "jump" slightly up and down on AltspaceVR cursor press and release.  It will also respond to corresponding HTML5 mouse events in a traditional browser.

**Step 6b**:
Add interactive behavior with [Cursor Effect Plugins]
```
var dragEffect = new DragPlaneEffect();
var blueGreen = new THREE.Color(0, 1, 1);
var hoverEffect = new ColorHoverEffect( blueGreen );

cursorEvents.addEffect( dragEffect, cube );
cursorEvents.addEffect( hoverEffect, cube );
```
Now the cube is draggable (using left mouse click) and it will also change color when the cursor hovers over it. In addition to using plugins included with this SDK, you can create your own, for use in your apps or to share with the AltspaceVR developer community.

**Step 7**:
Add muti-player networking with [FirebaseSync]
```
var firebaseRootURL = "https://your-firebase-root.firebaseio.com/";
var appId = "Your-App-Name";
firebaseSync = new FirebaseSync( firebaseRootURL, appId );
firebaseSync.addObject( cube, "cube" ); // object and unique id
firebaseSync.connect();
...
..
// after changing position.y of cube above
firebaseSync.saveObject( cube );
// or call firebaseSync.update() in your animate loop to save all objects,
// but not recommended if objects change position or rotation every frame.
```
The new object state is now saved to the [Firebase](http://firebase.com) cloud and broadcast to any clients connected to this room.  FirebaseSync will update your objects when it receives broadcasts from other clients.

Now this basic app is complete! For details, see the source code: [examples/spinning-cube.html].



[AltOBJMTLLoader]: https://github.com/AltspaceVR/AltspaceSDK/wiki/AltOBJMTLLoader
[AltRender]: https://github.com/AltspaceVR/AltspaceSDK/wiki/AltRenderer
[CursorEvents]: https://github.com/AltspaceVR/AltspaceSDK/wiki/CursorEvents
[ColorHighlightEffect]: https://github.com/AltspaceVR/AltspaceSDK/wiki/ColorHighlightEffect
[DragPlaneEffect]: https://github.com/AltspaceVR/AltspaceSDK/wiki/DragPlaneEffect
[FirebaseSync]: https://github.com/AltspaceVR/AltspaceSDK/wiki/FirebaseSync
[Three.js]: http://https://github.com/mrdoob/three.js/
[Workflow]: https://github.com/AltspaceVR/AltspaceSDK/wiki/Workflow
[Cursor Effect Plugins]: https://github.com/AltspaceVR/AltspaceSDK/wiki/Cursor-Effect-Plugins
[Prepros]: https://prepros.io/

[examples/spinning-cube.html]: examples/spinning-cube.html
[cube.obj]: examples/spinning_cube/cube.obj
[cube.mtl]: examples/spinning_cube/cube.mtl