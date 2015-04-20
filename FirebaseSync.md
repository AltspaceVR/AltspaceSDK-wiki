Synchronizes the positions of objects across the network. If one user moves a hologram, all other users in the room will see the object in the new position. This is currently done using the Firebase object database, so a  Firebase Account is required.  Sign up for free at Firebase.com and note your database URL, which is an argument to the FirebaseSync constructor.  

FirebaseSync implements the concept of a **room**, so that multiple instances of your app can be running simultaneously, each with its own set of objects.  You can specify the “room=roomX” parameter in your app URL, where X in an integer, or if you omit it a new room will be created.

**Constructor**

**Properties**

**Methods**


**Source**

* [FirebaseSync.js](https://github.com/AltspaceVR/AltspaceSDK/blob/master/src/sync/FirebaseSync.js)