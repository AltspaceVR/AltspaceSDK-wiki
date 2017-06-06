## Description
Geometry Count is the number of individual geometries rendered by your app. Geometry instances lead to additional draw calls when rendering your app. 

In some instances, geometry re-use can lead to further optimizations thanks to render batching, where objects with the same geometry are rendered in a single draw call.

Note: Geometry Count represents all the geometries you have ever renderered into the scene, even if you stop using the geometry later in the app's lifetime.

## Causes
High Geometry Count can be caused by poor re-use of geometries or if your app is continuously adding new geometries to the scene.

## Optimization
Re-use geometry instances as much as possible. Avoid cloning or duplicating geometries if they contain identical content.
If your app has many small geometries, merge them into a single, large geometry if possible.
