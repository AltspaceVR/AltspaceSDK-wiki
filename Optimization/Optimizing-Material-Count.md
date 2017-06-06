## Description
Material Count is the number of individual materials rendered by your app. Material instances lead to additional draw calls when rendering your app. 

> Material Count currently represents all the materials you have ever renderered into the scene, even if you stop using the material later in the app's lifetime.

## Causes
High Material Count can be caused by poor re-use of materials or if your app is continuously adding new materials to the scene.

## Optimization
Re-use material instances as much as possible. Avoid cloning or duplicating materials if they contain identical content.

In some instances, material re-use can lead to further optimizations thanks to render batching, where objects with the same material are rendered in a single draw call.
