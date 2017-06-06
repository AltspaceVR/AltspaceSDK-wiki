## Description
Triangle Count measures the total number of triangles in the geometry loaded by your app. High Triangle Count requires additional GPU resources to render and can also cause hitching at load-time.

> Note: The triangle count represents triangles of all the geometries you have ever renderered into the scene, even if you stop using the geometry later in the app's lifetime.

## Causes
High Triangle Count is caused by loading high-resolution models or by poor re-use of geometry instances.

## Optimization
Avoid high-resolution models. Decimate models before importing them in your app. Delete any hidden geometry. Re-use geometries instead of cloning/duplicating them.
