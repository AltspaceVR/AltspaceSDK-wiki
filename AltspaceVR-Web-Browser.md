AltspaceVR is a multi-user social virtual reality application that runs natively on Windows and Mac. It has a **built-in web browser** that allows users to experience 2D and 3D web content while in a 3D virtual reality environment networked with other users.  Below you will learn more about the Altspace Web Browser which is based on Chromium.

## Key Concepts

An **Altspace Web App** runs inside the AltspaceVR environment and utilizes APIs that are currently specific to Altspace.  Apps are built using Javascript and run inside the web browser (based on Chromium) that is running inside Altspace.  But the objects in your app are not limited to the 2D web browser, they are spawned into the 3D virtual environment. Your app’s objects may be called **holograms**, to distinguish them from the “permanent” objects that are part of the Altspace world.  Hologram transformations and interactions are managed by your application via javascript, while Altspace objects are managed by the Altspace application.

**Altspace APIs** are browser APIs that are specific to Altspace and exist on the `window.altspace` namespace.  These bindings are injected before any other Javascript on the page is executed. Note that these calls will not work in a normal web browser, so you will need to support multiple renderers and use input polyfills if you want your app to work in both a browser and inside Altspace.  The Altspace SDK provides some helper abstractions that work both inside and outside Altspace.

**Compositions** are the term we use for apps / games / videos / documents / images / sounds. Basically anything you would hit via a url and want to experience in altspace. (Think html ‘document’ or file).  **Enclosures** define a space where compositions can live, their dimensions in css pixels, and their scale. (Think ‘window’)  The reason we need new terminology is because compositions can contain 3D objects that are rendered in the virtual environment, unlike traditional web pages which are displayed on a 2D plane.

**Altspace Cursor** is that small blue dot that moves when you move your mouse.  Note that it moves in three dimensions, unlike a traditional mouse which only moves in the x,y plane. The two-dimensional mouse movements must be translated into the three-dimensional world-space, and this is done using raycast, like in typical 3D video games or other virtual environments. The origin of the ray is the player’s eye, a.k.a camera position, and the direction changes as the mouse moves. When the ray intersects an in-world object, such as a table, avatar, or hologram, the cursor is placed at the intersection point. 

Altspace enclosures have `innerWidth`, `innerDepth`, and `innerHeight` dimensions in CSS pixels.  Changes to any of these attributes triggers an onResize event, which is effectively a resolution change.  Resolution can change independently from the scale of the composition, which is obtained via the enclosure property `pixelsToMeter` (meaning CSS pixels, which is not a screen pixel but a unit of measure).  **Scaling** is an Altspace browser operation that does not happen in traditional web browsers, since the physical size of the computer screen does not change.  Currently at scale 1, 1000 pixels is a meter.  An app will not know it's scale directly, only the `pixelsToMeter` ratio, which you can use to make a hologram the approximate size as an in-world object, such as the avatar's head or hand.   

Your app can be in one of two states: **unsynced**, meaning only one person is seeing your app (like a traditional web page), or **synced**, meaning everyone is seeing the same initial url in the same place in the world.  However, everything beyond that (url changes, scrolling, events, etc) is a contract that the app needs to fulfill. We will be adding additional APIs in the future to make it easier for individual apps to fulfill this contract.

## Browser Limitations

* based on **Chromium 28** ([latest version][1] is 44 as of 4/14/2015)
* new tabs / windows not supported
* cannot print / download
* 3D CSS not supported
* Audio: no mp3 (unlike Chrome).  List of [Supported Media formats][2].
    * Please try to use only webaudio, if you use flash we will be sad, and support may be dropped in the future.
    * Your audio will sound like it is coming from the middle of your webpage.
* Traditional DOM is only on a single 2D quad right now, cannot be put on 3d objects.
