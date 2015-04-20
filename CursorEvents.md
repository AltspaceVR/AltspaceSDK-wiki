CursorEvents dispatches Altspace Cursor API events directly to the target object.  Like the AltOBJMTLLoader and AltRenderer instances, the CursorEvents instance is typically a singleton within your app.  

Cursor event names
* `holocursordown`: similar to mousedown, but only fired when cursor is over a hologram
* `holocursorup`: similar to mouseup, but only fired when cursor is over a hologram
* `holocursorenter`: similar to hoverOver, fired when cursor initially lands on a hologram
* `holocursorleave`: similar to hoverOut, fired when cursor stops landing on a hologram
* `holocursormove`: similar to mousemove, not related to a specific hologram

CursorEvents also manages effects, which make it easier to reuse event handling code. Multiple effects can be added to the same object, and multiple objects can be registered for the same effect (many-to-many).  You can create your own effects and also use pre-built effects which we call plugins.

**Constructor**

* CursorEvents ( parameters )
    * (optional) parameters {object} - properties to configure the instances
        * defaultTarget {object} - target object for the holocursormove event  
          (which is triggered on cursor movement, not object movement)  
          `cursorEvents = new CursorEvents( { defaultTarget: cube } );`

**Properties**

* defaultTarget {object} - target object for holocursormove event, set by constructor parameters.  Default is null.

**Methods**

* addObject ( object ) - any cursor events involving this object (previously loaded with AltOBJMTLLoader) will be dispatched directly to the object 
    * object {THREE.Object3D}
```js
var cursorEvents = new CursorEvents();
cursorEvents.addObject( cube ); 
object.addEventListener( "holocursordown", function( event ) {
    down-sound.play();
});

// instead of adding event listener to global window...
// window.addEventListener( "holocursordown", callback );
```

* addEffect( effect, object)
    * effect {object} - implements one of more of the cursor event callbacks.  Example: [ColorHighlightEffect]
    * object {THREE.Object3D} - object to which the effect will be applied.  
```js
var soundEffect = {
    holocursorenter: function( event ) { enter-sound.play() },
    holocursorleave: function( event ) { leave-sound.play() }
};
cursorEvents.addEffect( soundEffect, cube );

// or use cursor effect plugins
var effect = new ColorHighlightEffect();
cursorEvents.addEffect( cube, effect );
```

* enableMouseEvents( camera ) - when running in a traditional browser (not in Altspace), use [[AltObjectControls]] 
    * camera {[THREE.Camera]} - camera from the Three.js scene, used for raycasting.

* update() - should be called in your animation loop, mainly used to track the last position of the cursor.

**Related**
* Cursor event plugins including with this SDK: [[Cursor Effect Plugins]]
* Learn more about the Altspace Cursor on the [[Altspace Web Browser]] page.

**Source**

[src/cursor/CursorEvents.js](https://github.com/AltspaceVR/AltspaceSDK/blob/master/src/cursor/CursorEvents.js)

[THREE.Camera]: http://threejs.org/docs/#Reference/Cameras/Camera
[THREE.Object3D]: http://threejs.org/docs/#Reference/Core/Object3D