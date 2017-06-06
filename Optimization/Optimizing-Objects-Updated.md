## Description
Objects Updated counts the number of objects that have been updated since the last frame. An update consists of a change to an object's transform or its material's color.

> Note: The renderer flattens the scene hierarchy during a render call. This means that an update to a parent object's transform will cause updates to all of its descendant objects.

## Causes
Animating the transform or color of an object.

## Optimization
Try to minimize the number of animated objects in your scene.
