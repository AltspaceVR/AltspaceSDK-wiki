Synchronizes the positions of objects across the network. If one user moves a hologram, all other users in the room will see the object in the new position. Currently uses the Firebase object database.  Sign up for a free account at Firebase.com and note your database URL, passed to the FirebaseSync constructor.  

FirebaseSync implements the concept of a **room**, so that multiple instances of your app can be running simultaneously, each with its own set of objects.  You can specify the “room=roomX” parameter in your app URL, where X is an integer, or if you omit it a new room will be created.

Note that the `onConnectedCallback` will not be called until the connection to Firebase servers is made *and* any objects added via `addObject` have been synchronized.  This guarantees any initial game objects or "game state" objects are initialized, useful for "high score" or counting the number of times the app has been played in this room.

**Constructor**

* FirebaseSync( firebaseRootUrl, appId, parameters ) -
    * firebaseRootUrl {string} - example: "https://your-firebase-root.firebaseio.com/"
    * appId {string} - example: "MyAppName"
    * (optional) parameters {object} - properties to configure the instance
        * authToken {string} - content of a Firebase [custom authentication] token, passed to [authWithCustomToken]
        * authTokenPath {string} - location of an authToken, example: "./token.txt"
        * TRACE {boolean} - For debugging; if true, `console.log` Firebase events
          
**Properties**

* firebaseRootUrl {string} - set in constructor, URL of your firebase root
* appId {string} - set in constructor, allows you to host multiple apps per firebase root
* roomId {string} - either extracted from URL query string, or chosen randomly.
* roomURL {string} - obtained from Firebase; root URL of this room
* roomKey {string} - created by Firebase when room created, used in roomURL
* TRACE {boolean} - for debugging only; when true, console.log all Firebase events.

**Methods**

* connect( onConnectedCallback, addObjectCallback, removeObjectCallback ) - connect to Firebase and start listening for updates.  
    * (optional) onConnctedCallback {function} - called when connection is initialized
    * (optional) addObjectCallback {function} - called when a new synced object is created by a remote client   
    * (optional) removeObjectCallback {function} - called when a synced object is deleted by a remote client
    * Connect Handles these cases:
        * No roomID specified in URL: create room with random roomID and join it.
        * RoomID specified in URL, and room exists in DB: join it.
        * RoomID specified in URL, but room does not exists: create and join it.

* addObject( object, key ) - register this object for synchronization.
    * object {[THREE.Object3D]} - sync position, rotation, and scale for this object
    * key {string} - app-wide unique identifier for this object

* saveObject( object ) - save state of this object (broadcasts updates to all clients)
    * object {[THREE.Object3D]} - object to save (must `addObject` first)

* save() - save all objects that have changed since the last save  
  Note: If objects in your app are changing position or rotation every frame, calling this in your animate loop can lead to substantial network traffic due to sync events.


**Source**

* [src/sync/FirebaseSync.js](https://github.com/AltspaceVR/AltspaceSDK/blob/master/src/sync/FirebaseSync.js)

[THREE.Object3D]: http://threejs.org/docs/#Reference/Core/Object3D
[custom authentication]: https://www.firebase.com/docs/web/guide/login/custom.html
[authWithCustomToken]: https://www.firebase.com/docs/web/api/firebase/authwithcustomtoken.html
