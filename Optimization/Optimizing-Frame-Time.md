## Description
Frame Time measures how long, in milliseconds, it takes to process a single frame. This serves as an overall measure of your app's runtime performance. Frame Time is the inverse of FPS (frames per second).
Desktop PCs usually perform very well in this aspect, so this statistic is particularly useful on mobile devices.
Note: Frame Time includes time spent by Altspace itself. 

## Causes
Increased Frame Time mostly depends on the number of objects in your scene and how many of those objects are being updated continuously. If you're animating many objects or adding/removing many objects in your scene, Frame Time will be affected.

## Optimizations
Try to reduce the number of objects in your scene or the number of object changes.
