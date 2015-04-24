Synchronizes the positions of objects across the network. If one user moves a hologram, all other users in the room will see the object in the new position. Currently uses the Firebase object database.  Sign up for a free account at Firebase.com and note your database URL, passed to the FirebaseSync constructor.  

FirebaseSync implements the concept of a **room**, so that multiple instances of your app can be running simultaneously, each with its own set of objects.  You can specify the “room=roomX” parameter in your app URL, where X is an integer, or if you omit it a new room will be created.

**Constructor**

* FirebaseSync( firebaseRootUrl, appId, parameters ) -
    * firebaseRootUrl {string} - example: "https://your-firebase-root.firebaseio.com/"
    * appId {string} - example: "My-App-Name"
    * (optional) parameters {object} - properties to configure the instance
        * TRACE {boolean} - For debugging; if true, `console.log` Firebase events
          
**Properties**

* firebaseRootUrl {string} - set in constructor, URL of your firebase root
* appId {string} - set in constructor, allows you to host multiple apps per firebase root
* roomId {string} - either extracted from URL query string, or chosen randomly.
* roomURL {string} - obtained from Firebase; root URL of this room
* roomKey {string} - created by Firebase when room created, used in roomURL
* TRACE {boolean} - for debugging only; when true, console.log all Firebase events.

**Methods**

* addObject( object, key ) - register this object for synchronization
    * object {[THREE.Object3D]} - sync position, rotation, and scale for this object
    * key {string} - app-wide unique identifier for this object

    Currently, `addObject` must be called on any objects in your scene that you want to sync *before* calling connect().

* connect( onCompleteCallback ) - connect to Firebase and start listening for updates
    * onCompleteCallback {function} - called when connection is initialized  
    * Connect Handles these cases:
        * No roomID specified in URL: create room with random roomID and join it.
        * RoomID specified in URL, and room exists in DB: join it.
        * RoomID specified in URL, but room does not exists: create and join it.

* saveObject( object ) - save state of this object (broadcasts updates to all clients)
    * object {[THREE.Object3D]} - object to save (must `addObject` first)

* save() - save all objects that have changed since the last save  
  Note: If objects in your app are changing position or rotation every frame, calling this in your animate loop can lead to substantial network traffic due to sync events.


**Source**

* [src/sync/FirebaseSync.js](https://github.com/AltspaceVR/AltspaceSDK/blob/master/src/sync/FirebaseSync.js)

[THREE.Object3D]: http://threejs.org/docs/#Reference/Core/Object3D
