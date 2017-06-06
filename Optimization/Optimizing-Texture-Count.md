## Description
The number of textures loaded by your appTexture instances lead to additional draw calls when rendering your app.

> The texture count represents all the textures you have ever renderered into the scene, even if you stop using the texture later in the app's lifetime.

## Causes

High Texture Count can be caused by poor re-use of textures or if your app is continuously loading new textures into the scene. Some models may reference many textures in ways that may not be obvious, especially if the mesh + textures are bundled into a single file. 

## Optimization
Re-use texture instances as much as possible. Avoid cloning or duplicating textures if they share content and properties that never change.

In some instances, texture re-use can lead to further optimizations thanks to render batching, where objects with the same 
texture are rendered in a single draw call.

Use texture atlasing with texture offsets where possible. 
This would allow you to use a single texture to represent different objects.

Use lightmaps instead of baking lighting onto the texture map.

