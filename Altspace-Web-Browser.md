AltspaceVR is a multi-user social virtual reality application that runs natively on Windows and Mac. It has a **built-in web browser** that allows users to experience 2D and 3D web content while in a 3D virtual reality environment networked with other users.  Below you will learn more about the Altspace Web Browser (see also [[Known Issues]] page for current limitations), which is based on the Chromium web browser.

## Key Concepts

An **Altspace Web App** runs inside the AltspaceVR environment and utilizes APIs that are currently specific to Altspace.  Apps are built using Javascript and run inside the web browser (based on Chromium) that is running inside Altspace.  But the objects in your app are not limited to the 2D web browser, they are spawned into the 3D virtual environment. Your app’s objects may be called **holograms**, to distinguish them from the “permanent” objects that are part of the Altspace world.  Hologram transformations and interactions are managed by your application via javascript, while Altspace objects are managed by the Altspace application.

**Altspace APIs** are browser APIs that are specific to Altspace, many of which appear on the window.Alt namespace (others may appear elsewhere, like window.innerDepth).  These bindings are injected before any other Javascript on the page is executed. Note that these calls will not work in a normal web browser, so you will need to polyfill if you want your app to work in both a browser and inside Altspace.  The Altspace SDK provides some components that work both inside and outside Altspace and provides an abstraction on top of the Altspace API that many developers have found useful.

**Compositions** are the term we use for apps / games / videos / documents / images / sounds. Basically anything you would hit via a url and want to experience in altspace. (Think html ‘document’ or file).  **Enclosures** define a space where compositions can live, their dimensions in css pixels, and their scale. (Think ‘window’)  The reason we need new terminology is because compositions can contain 3D objects that are rendered in the virtual environment, unlike traditional web pages which are displayed on a 2D plane.

**Altspace Cursor** is that small blue dot that moves when you move your mouse.  Note that it moves in three dimensions, unlike a traditional mouse which only moves in the x,y plane. The two-dimensional mouse movements must be translated into the three-dimensional world-space, and this is done using raycast, like in typical 3D video games or other virtual environments. The origin of the ray is the player’s eye, a.k.a camera position, and the direction changes as the mouse moves. When the ray intersects an in-game object, the cursor is placed at the intersection point. 

Differences from traditional browsers:
* ‘css pixels’ are not actual pixels, but units
* ‘css pixel’ = px in any <length> definition (like width)
* Resolution (like resizing a window) can change independently of scale of objects
* window.innerDepth, in addition to innerWidth and innerHeight
* pixelToMeterRatio (only from JS right now)
* devicePixelRatio is always 1 right now
* at scale 1, 1000 pixels is a meter
* the web app will not actually know it’s scale, but it will know it’s pixelToMeterRatio

Your app can be in one of two states:

* Unsynced: Only one person is seeing your app, this is like a normal web page.
* Synced: Everyone is seeing the same initial url, in the same place in the world, everything beyond that (url changes, scrolling, events, etc) is a contract that the app needs to fulfill. We will be adding additional APIs in the future to make it easier for individual apps to fulfill this contract.
