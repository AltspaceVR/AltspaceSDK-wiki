
### AltObjectControls
AltObjectControls extends [ObjectControls], an open-source library for interacting with ThreeJS objects using a mouse or other input device, to work with Altspace cursor events. The advantage of using AltObjectControls is your app will respond appropriately to both cursor events when running in Altspace and mouse events when running the web browser.  Typically you will not create the AltObjectControls instance or call its methods directly, as it is managed by the CursorEvents (see above). The key method is `CursorEvents.enableMouseEvents()`. 

### FirebaseSync
FirebaseSync synchronizes the positions of objects across the network. If one user moves a hologram, all other users in the room will see the object in the new position. This is currently done using the Firebase object database, so a  Firebase Account is required.  Sign up for free at Firebase.com and note your database URL, which is an argument to the FirebaseSync constructor.  

FirebaseSync implements the concept of a **room**, so that multiple instances of your app can be running simultaneously, each with its own set of objects.  You can specify the “room=roomX” parameter in your app URL, where X in an integer, or if you omit it a new room will be created.

Methods:
* `new FirebaseSync( firebaseRootUrl, appId )`: create the singleton (but do not connect yet)
    * firebaseRootUrl example: "https://your-firebase-root.firebaseio.com/"
    * appId example: "Your-App-Name"
    * app url will be: "https://your-firebase-root.firebaseio.com/Your-App-Name"
* `add( object )`: Call for all objects (THREE.Object3D) that you want to get synchronized
* `connect()`: connect to the remote server and synchronize initial object states.  
* `saveObject( object )`: save current state of object and broadcast to all other clients.

Currently you must call add() for all objects before calling connect(), as new synced objects can only be created during the initialization phase, and not while your app is running.  (We plan to remove this limitation soon)


[Repo README]: https://github.com/AltspaceVR/AltspaceSDK
[ObjectControls]: https://github.com/cabbibo/ObjectControls
[DragPlaneEffect]: ../../src/DragPlaneEffect.js