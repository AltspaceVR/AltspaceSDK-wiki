Geometry instances lead to additional draw calls when rendering your app. Re-use geometry instances as much as possible.
Avoid cloning or duplicating geometries if they share content and properties that never change.

In some instances, geometry re-use can lead to further optimizations thanks to render batching, where objects with the same texture are rendered in a single draw call.

Merge individual geometries if possible.
