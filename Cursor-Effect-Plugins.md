Cursor Effect Plugins may be used with the CursorEvents manager (see [[SDK Guide]] for details, and [Repo README] for an example).  Just "plugin" the effects below to add interactive behaviors to your app objects.

## ColorHighlightEffect

Simple effect that changes the color of an object on "hover over", and reverts back to the original color on "hover out" (holocursorenter / holocursorleave events).  You can select the highlight color by passing it as an argument to the constructor, if not a default highlight color is used. 

## DragEffect

A more complicated effect that implements drag-and-drop of objects. Click once to start drag, click again to release (holocursorup / holocursordown events).  Currently the drag movement is limited to an x-z plane parallel to the floor. You can select a drag plane (THREE.Mesh with BoxGeometry) by passing it as parameter to the constructor, if not a default one will be created for you. You can also include the firebaseSync instance, if you want to sync an object after its position changes due to a drag.


[Repo README]: https://github.com/AltspaceVR/AltspaceSDK
