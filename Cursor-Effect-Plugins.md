Cursor Effect Plugins may be used with the [[CursorEvents]] manager.  Just "plugin" the effects below to add interactive behaviors to your app objects.  Since you only need to create the instance, than add it to an object using `CursorEvents.addEffect` in most cases only the constructors are listed below.

### ColorHighlightEffect

Simple effect that changes the color of an object on "hover over", and reverts back to the original color on "hover out" (holocursorenter / holocursorleave events).  Works both in Altspace and traditional browsers.  

ColorHighlightEffect( parameters )
* (optional) parameters {object} - properties to configure color settings
    * color {THREE.Color} - highlight color to use; set as object.userData.tintColor in Altspace.  Defaults to yellow: `THREE.Color(1, 1, 0)` 

Example: [/src/examples/spinning-cube.html](https://github.com/AltspaceVR/AltspaceSDK/blob/master/examples/spinningcube.html), in function `initEvents()`  
Source: [src/cursor/ColorHighlightEffect.js](https://github.com/AltspaceVR/AltspaceSDK/blob/master/src/cursor/ColorHoverEffect.js)

### DragPlaneEffect

A more complicated effect that implements drag-and-drop of objects. Click once to start drag, click again to release (holocursorup / holocursordown events).  Currently the drag movement is limited to an x-z plane parallel to the floor.  Works both in Altspace and traditional browsers.

DragPlaneEffect( parameters )
* (optional) parameters {object} - properties to configure drag settings
    * dragPlane {[THREE.Mesh]} - mesh (does not need to be added to the scene) with [THREE.BoxGeometry], its position and width/depth should match the drag area of your scene.  If omitted, a default one is created for you:  
    `new THREE.Mesh( new THREE.BoxGeometry(500, 0.25, 500),
                     new THREE.MeshBasicMaterial( { transparent: true, opacity: 0.25 }));`
    * firebaseSync {[[FirebaseSync]]} - used to save an object as its position changes due to a drag.  Not needed if you are using `FirebaseSync.saveAll()`
    * dragPointMarker {[THREE.Mesh]} - For degbugging; mark the raycast intersection point on drag and hoverOver. Mesh with SphereGeometry works well.

Example: [/src/examples/spinning-cube.html](https://github.com/AltspaceVR/AltspaceSDK/blob/master/examples/spinningcube.html), in function `initEvents()`  
Source: [src/cursor/DragPlaneEffect.js](https://github.com/AltspaceVR/AltspaceSDK/blob/master/src/cursor/DragPlaneEffect.js)
 

[Repo README]: https://github.com/AltspaceVR/AltspaceSDK
[THREE.Color]: http://threejs.org/docs/#Reference/Math/Color
[THREE.Mesh]: http://threejs.org/docs/#Reference/Objects/Mesh
[THREE.BoxGeometry]: http://threejs.org/docs/#Reference/Extras.Geometries/BoxGeometry
