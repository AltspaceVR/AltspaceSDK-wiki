In order for an object to appear in Altspace, it must be loaded by your app using the AltOBJMTLLoader. The object geometry and materials are defined by the OBJ and MTL files (which are assumed to have the same basenames). The loader parses these two ASCII text files and creates a ThreeJS object. Finally, it attaches a special attribute that notifies the AtlRender that this object corresponds to a hologram in Altspace, and thus should be included in the serialized scene passed to the Unity engine.  Note that loading a model can take a half-second, and you will probably want to wait until all needed objects are loaded before continuing with your app initialization.

**Constructor**

* AltOBJMTLLoader( manager )

    * manager {[LoadingManager]} — The loadingManager for the loader to use. Default is [THREE.DefaultLoadingManager].

**Properties**

* .inAltspace {boolean} - Set to true if running in the [[Altspace Web Browser]].

**Methods**

* load( objUrl, onLoad, onProgress, onError )
    * objUrl {string} - Path to the file.  
      example: `models/cube.obj` and note `models/cube.mtl` must also exist.
    * onLoad {function} - Function called when loading is done. 
    * onProgress {function} - Function called when an item is loaded.  
      (Note an .mtl file may specify multiple texture files to be loaded).
    * onError {function} - Function called if an item failed to be loaded.

**Source**
* [src/AltOBJMTLLoader.js](https://github.com/AltspaceVR/AltspaceSDK/blob/master/src/AltOBJMTLLoader.js)

[LoadingManager]: http://threejs.org/docs/#Reference/Loaders/LoadingManager
[THREE.DefaultLoadingManager]: http://threejs.org/docs/#Reference/Loaders/LoadingManager


