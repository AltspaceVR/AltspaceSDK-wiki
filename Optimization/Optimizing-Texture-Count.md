Texture instances lead to additional draw calls when rendering your app.
Re-use texture instances as much as possible. Avoid cloning or duplicating textures if they share content and properties that never change.

In some instances, texture re-use can lead to further optimizations thanks to render batching, where objects with the same 
texture are rendered in a single draw call.

Use texture atlasing with texture offsets where possible. 
This would allow you to use a single textureto represent different objects.

Use lightmaps instead of baking lighting onto the texture map.

Note: The texture count represents all the textures you have ever renderered into the scene, even if you stop using the texture later in the app's lifetime.
