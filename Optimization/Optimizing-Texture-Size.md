## Description
Texture Size measures the total size, in pixels, of all of the textures you've loaded into your app. Large textures can cause hitching during load-time.

> Note: Texture Size represents all the textures you have ever renderered into the scene, even if you stop using the texture later in the app's lifetime.

## Causes
High Texture Size can be caused by overly-large textures or poor re-use of textures.

## Optimization
Avoid using large textures if you can get away with smaller ones. Generally speaking, texture size should be proportional to the size of the object in-game.
