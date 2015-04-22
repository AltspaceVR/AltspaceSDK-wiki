Helper for loading multiple models, sequentially or in parallel. 

**Constructor**

None. Instance created when script is imported (uses Javascript [Module Pattern](http://toddmotto.com/mastering-the-module-pattern/)).

**Methods**

* loadFilesInParallel( fileList, cb, optionalLoader ) - for loading many different objects
    * fileList {array} - list containing one item (such as `fileParams` below) for each file
    * cb {function} - called when all files are loaded
    * (optional) optionalLoader {function} - function called for each item in fileList. Default is MultiLoader.loadModel, which uses `THREE.AltOBJMTLLoader`.

* loadFilesInSeries( fileList, cb, optionalLoader ) - for loading many of the same object
    * same parameters as `loadFilesInParallel` above

* loadModel( fileParams, cb ) - the default file loader, called for each file in fileList.
    * fileParams {object} - object with two properties: fileName and cacheKey
        * fileName {string} - path to the OBJ file, such as "/models/cube.obj"
        * cacheKey {string} - id for this object, such as "cube-1", must be unique among all objects loaded by MultiLoader. Needed to differentiate between multiple objects loaded from same fileName. 
    * cb {function} - called when all files finished loading

* getCached( cacheKey ) - Retrieve the cached object. Returns null if the item does not exist. 
    * cacheKey {string} - object id, passes as parameter when it was initially loaded.

**Example**

[src/examples/dice-grid.html](https://github.com/AltspaceVR/AltspaceSDK/blob/master/examples/dice-grid.html)

**Source**

[src/helpers/MultiLoader.js](https://github.com/AltspaceVR/AltspaceSDK/blob/master/src/helpers/MultiLoader.js)

