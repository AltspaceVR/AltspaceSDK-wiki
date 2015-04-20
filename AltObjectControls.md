AltObjectControls is used internally by [[CursorEvents]] (see method `enableMouseEvents`) so generally you will **not need to instantiate this class directly**.

AltObjectControls extends [ObjectControls], an open-source library for controlling ThreeJS objects using a mouse or other input device, to work with Altspace cursor events. The advantage of using AltObjectControls is your app will respond appropriately to both cursor events when in Altspace and mouse events when in a traditional browser. 

**Source**

[src/cursor/AltObjectControls.js](https://github.com/AltspaceVR/AltspaceSDK/blob/master/src/cursor/AltObjectControls.js)

[ObjectControls]: https://github.com/cabbibo/ObjectControls

