CursorEvents dispatches Altspace Cursor API events directly to the target object. (Learn more about the Altspace Cursor on the [[Altspace Web Browser]] page.)  Like the AltOBJMTLLoader and AltRenderer instances, the CursorEvents instance is typically a singleton within your app.  

```
var cursorEvents = new CursorEvents();
cursorEvents.addObject( object );   // register to receive cursor events
object.addEventListener( "holocursordown", onDownCallback );

// above "object" was loaded with OBJMTLLoader
```

CursorEvents also manages effects, which make it easier to reuse event handling code.  Instead of putting your event handlers inline with the rest of your application, you can put them in a separate file.  Using this modular approach also lets you reuse effects, either created by you for another app, or by other developers in your organization or in the Altspace developer community. You can have multiple effects added to the same object, and multiple objects that are registered for the same effect (many-to-many relationship).  To create effects, simply implement the Cursor Event callbacks that your effect requires, or use pre-built effects which we call plugins.  Plugins including with with SDK: [[ColorHighlightEffect]], [[DragPlaneEffect]].

```
var effect = new ColorHighlightEffect();
cursorEvents.addEffect( object, effect );
```

Constructor

TODO

Properties

TODO

Methods

TODO

Source

[src/cursor/CursorEvents.js](https://github.com/AltspaceVR/AltspaceSDK/blob/master/src/cursor/CursorEvents.js)
