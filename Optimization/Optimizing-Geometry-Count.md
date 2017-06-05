Geometry instances lead to additional draw calls when rendering your app. Re-use geometry instances as much as possible.
Avoid cloning or duplicating geometries if they share content and properties that never change.

In some instances, geometry re-use can lead to further optimizations thanks to render batching, where objects with the same geometry are rendered in a single draw call.

If your app has many small geometries, merge them into a single, large geometry if possible.

Note: The geometry count represents all the geometries you have ever renderered into the scene, even if you stop using the geometry later in the app's lifetime.
