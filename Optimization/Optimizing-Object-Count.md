## Description
Object Count is the number of individual objects (i.e. meshes) in your scene. High Object Count can lead to runtime performance issues. Animated objects are certainly more expensive but event static objects require processing on every frame.
Object Count can also affect load-time performance.

## Causes
High Object Count can be caused by loading large models, that are composed of many separate meshes, into a scene. Your app may also be creating new meshes when it ought to reuse existing meshes.

## Optimization
Design your app so that it does not require many individual objects.
One strategy for reducing object count is to merge static objects into a single mesh when possible.
You can also hide and show objects from an object pool instead of creating entirely new ones.
