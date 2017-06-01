App performance can be affected by the number of objects in your scene.
Animated objects are certainly more expensive but event static objects require processing on every frame.

Design your app so that it does not require many individual objects.
One strategy for reducing object count is to merge static objects into a single mesh when possible.
