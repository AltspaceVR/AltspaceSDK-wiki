Constructor

* THREE.AltRenderer ()

Properties

* .inAltspace {boolean} - Set to true if running in the [[Altspace Web Browser]].

Methods

* render( scene ) - render all objects in the scene that were loaded with the [[AltOBJMTLLoader]]. Usually called in the animation loop.  
    * scene {[THREE.Scene]} - Three.js scene containing the objects to be rendered.  

Source

* [src/AltRenderer.js](https://github.com/AltspaceVR/AltspaceSDK/blob/master/src/AltRenderer.js)

[THREE.Scene]: http://threejs.org/docs/#Reference/Scenes/Scene
