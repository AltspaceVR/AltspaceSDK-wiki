The purpose of the Altspace Apps SDK is to help you more easily write cool games and other apps that run in Altspace.  This guide explains the features of the SDK. For a quick Getting Starting overview, see the [Repo README].

## SDK Components
Below are the current components of the SDK.  AltRender and AltOBJMTLLoader are required by all Altspace Apps; others are optional.

### AltRender
The AltRender forms the link between the ThreeJS scene and the Altspace virtual world.  It packages all the necessary data about the scene, including the position, rotation, scale, and source URL of all objects.  Instead of using the WebGLRenderer, as you would for existing ThreeJS apps, in Altspace you will want to use the AltRender.  

If you only plan to run and develop your app inside Altspace, this is the only renderer you need. If you want your app to run in traditional web browsers as well,you will need to detect which environment is present and create the correct renderer.  Unlike the WebGLRenderer constructor that takes the scene and camera as arguments, the AltRender constructor requires only the scene, since the camera is managed by Altspace (but you can pass the camera as a second argument which will be ignored).  After that, simply call the render() method in your animation loop as normal.   Note that render is the only method currently supported, so you should avoid calling setSize, setClearColor, or other methods when using the AltRender. 


### AltOBJMTLLoader
In order for an object to appear in Altspace, it must be loaded by your app using the AltOBJMTLLoader.  The object geometry and materials are defined by the OBJ and MTL files (which are assumed to have the same basenames).  The loader parses these two ASCII text files and creates a ThreeJS object.  Finally, it attaches a special attribute (described in the Altspace API section below) that notifies the AtlRender that this object corresponds to a hologram in Altspace, and thus should be included in the serialized scene passed to the Unity engine.  Note that loading a model can take a half-second, and you will probably want to wait until all needed objects are loaded before continuing with your app initialization, for example by using an interval timer.

### CursorEvents
CursorEvents dispatches Altspace Cursor API events directly to the target object. (The Altspace Cursor is described on the [[Altspace Web Browser]] page.)  Thus you can attach event listeners to objects instead of the window element.  CursorEvents takes care of setup and dispatch tasks, such as adding event listeners the the web page context and mapping between object identifiers (uuid) returned by Altspace events to ThreeJS objects in your scene.  Optionally, CursorEvents can also manage CursorEffects and AltObjectControls, described next.

### CursorEffects
CursorEffects works with CursorEvents and makes it easier to reuse event handling code.  For simple interactions, like a change-object-color hover effect, this might not be necessary, but for more complicated interactions like drag-and-drop it can be useful to isolate this logic in a separate file, instead of putting it inline with the rest of your application.  Steps for using CursorEffects:

1. cursorEvents.enableEffects() - This will create the CursorEffects manager for you, and add it to the CursorEvents manager.
2. Create an effect that implements callbacks for the events you want to handle (for example, PlaySoundEffect.hoverOver)
3. cursorEvents.addEffect(object, effect) - specifies the effect you want to use, and the object to which you want it to be applied.  You can have multiple effects added to the same object, and multiple objects that are registered for the same effect (many-to-many relationship).  
4. cursorEvents.update() in your animate loop, which envokes update() on all your effects that define it.

Using this modular approach also lets you reuse effects, either created by you for another app, or by other developers in your organization or in the Altspace developer community.  The Altspace SDK includes these effects:
* **ColorHighlightEffect** - Simple effect that changes the color of an object on hoverOver, and reverts back to the original color on hoverOut.  You can select the highlight color by passing it as an argument to the constructor.  
* **DragEffect** - A more complicated effect that implements drag-and-drop of objects.  Currently the drag movement is limited to an x-z plane parallel to the floor (since it was originally developed for a chess game) but it can be adapted to drag along an x-y plane.   

### AltObjectControls
AltObjectControls extends ObjectControls, an open-source library for interacting with ThreeJS objects using a mouse or other input device, to work with Altspace cursor events. The advantage of using AltObjectControls is your app will respond appropriately to both cursor events when running in Altspace and mouse events when running the web browser. To use: call cursorEvents.enableMouseEvents( camera ) and the CursorEvents manage will create the AltObjectControls instance for you.

### FirebaseSync
FirebaseSync synchronizes the positions of objects across the network so that if one user moves a hologram, all other users in the room will see the object in the new position.  Synchronization is currently done using the Firebase object database, so a  Firebase Account is required.  Sign up for free at Firebase.com and note your database URL, which is an argument to the FirebaseSync constructor.  You can specify the “room=roomX” parameter in your app URL, X between 0 and 1000, or if you omit it a new room will be created.  Currently there is no relationship between the Firebase rooms and Altspace rooms.  

There are three steps to use FirebaseSync: 

1. create the instance, passing your Firebase root URL as an argument
2. add( object ) all THREE.Object3D objects that you want to get synchronized.
3. connect() to connect to the remote server and synchronize the object positions.  
4. saveObject( object ) when you change the position or rotation of an object, and the change will be broadcast to all other clients connected to this room

[Repo README]: https://github.com/AltspaceVR/AltspaceSDK
