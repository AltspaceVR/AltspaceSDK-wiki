Synchronizes the positions of objects across the network. If one user moves a hologram, all other users in the room will see the object in the new position. This is currently done using the Firebase object database, so a  Firebase Account is required.  Sign up for free at Firebase.com and note your database URL, which is an argument to the FirebaseSync constructor.  

FirebaseSync implements the concept of a **room**, so that multiple instances of your app can be running simultaneously, each with its own set of objects.  You can specify the “room=roomX” parameter in your app URL, where X in an integer, or if you omit it a new room will be created.

**Constructor**

* FirebaseSync( firebaseRootUrl, appId, parameters ) -
    * firebaseRootUrl {string} - example: "https://your-firebase-root.firebaseio.com/"
    * appId {string} - example: "My-App-Name"
    * parameters {object} - properties to initialize the instance
        * syncUserDataProps {array} - list of which properties to sync in THREE.Object3D.userData  
          (for example,  `syncUserDataProps = [ "gameState" ]` )
          
**Properties**

* firebaseRootUrl {string} - set in constructor, URL of your firebase root
* appId {string} - set in constructor, allows you to host multiple apps per firebase root
* roomId {string} - either extracted from URL query string, or chosen randomly.
* roomURL {string} - obtained from Firebase; root URL of this room
* roomKey {string} - created by Firebase when room created, used in roomURL
* TRACE {boolean} - for debugging only; when true, console.log all Firebase events. Default is false.

**Methods**


**Source**

* [src/sync/FirebaseSync.js](https://github.com/AltspaceVR/AltspaceSDK/blob/master/src/sync/FirebaseSync.js)