## Description
Frame time (the inverse of FPS) is an overall measure of your app's performance. 
Desktop PCs usually perform very well in this aspect, so this statistic is particularly useful on mobile devices.
Note that frame time includes time spent by Altspace itself. 

## Causes
Increased frame time mostly depends on the number of objects in your scene and how many of those objects are being updated continuously. If you're animating many objects or adding/removing many objects in your scene, frame time will be affected.

## Optimizations
Try to reduce the number of objects in your scene or the number of object changes.
