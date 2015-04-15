This guide explains the features of the Altspace Web App SDK.  See the [Repo README], which walks through building a sample app, before diving into the details below.

## SDK Components
The current components of the SDK are as follows. 

* Core: 
  * AltOBJMTLLoader
  * AltRenderer
* Cursor: 
  * CursorEvents
  * CursorEffects
  * AltObjectControls
* Sync: 
  * FirebaseSync

In addition, we provide optional [[Cursor Effect Plugins]].


### AltOBJMTLLoader
In order for an object to appear in Altspace, it must be loaded by your app using the AltOBJMTLLoader.  The object geometry and materials are defined by the OBJ and MTL files (which are assumed to have the same basenames).  The loader parses these two ASCII text files and creates a ThreeJS object.  Finally, it attaches a special attribute  that notifies the AtlRender that this object corresponds to a hologram in Altspace, and thus should be included in the serialized scene passed to the Unity engine.  

Methods:
* `new THREE.AltOBJMTLLoader()`: called to create the singleton used to load multiple objects.
* `load(filename, onLoadCallback)`: Imports the OBJ file at filename, and envokes onLoadCallback when done.

Note that loading a model can take a half-second, and you will probably want to wait until all needed objects are loaded before continuing with your app initialization, for example by using an interval timer.

### AltRender
The AltRender forms the link between the ThreeJS scene and the Altspace virtual world.  It packages all the necessary data about the scene, including the position, rotation, scale, and source URL of all objects.  Instead of using the WebGLRenderer, as you would for existing ThreeJS apps, in Altspace you will want to use the AltRender.  

Methods:
* `new THREE.AltRenderer()`: called during scene initialization to create the singleton.
* `render( scene )`: Render the scene; call every frame in your animation loop (via requestAnimationFrame).

Note that AltRender constructor requires only the scene, since the camera is managed by Altspace, unlike the WebGLRenderer constructor that takes the scene and camera as arguments.   Note also that render is the only method currently supported, so you should avoid calling setSize, setClearColor, or other methods when using the AltRender.  If you only plan to run and develop your app inside Altspace, this is the only renderer you need. If you want your app to run in traditional web browsers as well,you will need to detect which environment is present and create the correct renderer.  

### CursorEvents
CursorEvents dispatches Altspace Cursor API events directly to the target object. (The Altspace Cursor is described on the [[Altspace Web Browser]] page.)  Thus you can attach event listeners to objects instead of the window element.  CursorEvents takes care of setup and dispatch tasks, such as adding event listeners the the web page context and mapping between object identifiers (uuid) returned by Altspace events to ThreeJS objects in your scene. 

Like the AltOBJMTLLoader and AltRenderer instances, the CursorEvents instance is typically a singleton within your app.  It can also manage the CursorEffects and AltObjectController singletons, described in following sections.

Methods:
* `new CursorEvents()`: constructor
* `add( object )`: register the object to receive cursor events
    * then attach event listeners to the object, for example:
    * `object.addEventListener( "holocursordown", callback )`;
    * in addition to attaching event listeners directly, use pre-defined CursorEffects
* `enableEffects()`: create an internal instance of CursorEffects (see below)
* `addEffect( object, effect )`: register the cursor effect you want to use, and the object to which you want it to be applied.  
* `enableMouseEvents( camera )`: create an internal instance of AltObjectControls (see below)
* `update()`: update the CursorEffects and AltObjectControls instances; call every frame in your animation loop.

Cursor events
* holocursordown: similar to mousedown, but only fired when cursor is over a hologram
* holocursorup: similar to mouseup, but only fired when cursor is over a hologram
* holocursorenter: similar to hoverOver, fired when cursor initially lands on a hologram
* holocursorleave: similar to hoverOut, fired when cursor stops landing on a hologram
* holocursormove: similar to mousemove**

**Unlike the other events, holocursormove is not tied to a specific hologram.  To receive this event provide a default target in the CursorEvents constructor. You can also add listeners for cursor events directly to the global window element, such as `window.addEventListener( "holocursormove", callback )`

### CursorEffects
CursorEffects works with CursorEvents and makes it easier to reuse event handling code.  For simple interactions, like a change-object-color hover effect, this might not be necessary, but for more complicated interactions like drag-and-drop it can be useful to isolate this logic in a separate file, instead of putting it inline with the rest of your application.  Using this modular approach also lets you reuse effects, either created by you for another app, or by other developers in your organization or in the Altspace developer community.

In most cases you will not create the CursorEffects instance or call its methods directly, as it is managed by the CursorEvents (see above).  The key method is `CursorEvents.addEffect(object, effect)`. You can have multiple effects added to the same object, and multiple objects that are registered for the same effect (many-to-many relationship).  To create effects, simply implement the Cursor Event callbacks that your effect requires, or use pre-built effects which we call plugins.  

See the [[Cursor Effect Plugins]] page for effect plugins included with this SDK.

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

This concludes the SDK Guide.  Return to the Wiki [[Home]]

[Repo README]: https://github.com/AltspaceVR/AltspaceSDK
[ObjectControls]: https://github.com/cabbibo/ObjectControls