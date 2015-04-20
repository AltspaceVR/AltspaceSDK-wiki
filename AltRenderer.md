The AltRender forms the link between the ThreeJS scene and the Altspace virtual world. It packages all the necessary data about the scene, including the position, rotation, scale, and source URL of all objects. Instead of using the WebGLRenderer, as you would for existing ThreeJS apps, in Altspace you will want to use the AltRender.

Note that AltRender constructor requires only the scene, since the camera is managed by Altspace, unlike the WebGLRenderer constructor that takes the scene and camera as arguments. Note also that render is the only method currently supported, so you should avoid calling setSize, setClearColor, or other methods when using the AltRender. If you only plan to run and develop your app inside Altspace, this is the only renderer you need. If you want your app to run in traditional web browsers as well,you will need to detect which environment is present and create the correct renderer.

**Constructor**

* THREE.AltRenderer ()

**Properties**

* .inAltspace {boolean} - Set to true if running in the [[Altspace Web Browser]].

**Methods**

* render( scene ) - render all objects in the scene that were loaded with the [[AltOBJMTLLoader]]. Usually called in the animation loop.  
    * scene {[THREE.Scene]} - Three.js scene containing the objects to be rendered.  

**Source**

* [src/AltRenderer.js](https://github.com/AltspaceVR/AltspaceSDK/blob/master/src/AltRenderer.js)

[THREE.Scene]: http://threejs.org/docs/#Reference/Scenes/Scene
