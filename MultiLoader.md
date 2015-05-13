Helper for loading multiple models, sequentially or in parallel. 

**Constructor**

None. Instance created when script is imported (uses Javascript [Module Pattern](http://toddmotto.com/mastering-the-module-pattern/)).

**Methods**

* load (fileList, cb) - loads the assets as sepcified in the fileList. Will execute the specified callback with an object containing all the assets loaded.
    * fileList {array} - array of objects containing the file to be loaded and a unique key. Example: {file: "path/to/file.obj", key: "some_identifier"}
    * cb {function} called when the assets are finished loading. Will pass an argument which a dictionary (object) of the loaded assets (keyed by the key specified in the fileList).

**Example**

[src/examples/dice-grid.html](https://github.com/AltspaceVR/AltspaceSDK/blob/master/examples/dice-grid.html)

**Source**

[src/helpers/MultiLoader.js](https://github.com/AltspaceVR/AltspaceSDK/blob/master/src/helpers/MultiLoader.js)

