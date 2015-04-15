This page describes the typical workflow for developing an Altspace Web App.

## Requirements Overview

Hardware Requirements
* Oculus Rift DK2 (for VR mode; developing in non-VR mode also supported)
* Windows or Mac laptop or desktop computer
* Dedicated GPU (for high-performance graphics)

Note the above requirements are for developing Altspace apps, not for simply running Altspace, which can be done on computers without a dedicated GPU.  The additional graphics power is needed when developing apps since you will also be running additional debugging tools, described below. (Integrated graphics *may* work, although not officially supported.)

Some hardware platforms successfully used for bulding Altspace Apps:
* Macbook Pro 15" laptop (i7/GT 750M)
* Alienware 13" laptop (i5/GTX 860M)

Required Software:
* [AltspaceVR client]: executable; note that access to Altspace client source code is not required.
* [Prepros]: Web development tool with integratd web server and automatical page reloading.
* [Sublime Text Editor]: Recommended, but you can use any editor or IDE that supports Javascript.
* Coherent Debugger: Allows you to see the console output of your Altspace web app (download link?)
    * on Mac: cannot rename it from Debugger.app after you extract it, or it won't run
    * due to its reliance on legacy .app bundle structure -- it needs an Info.plist with metadata.
* [GitHub Client]: A command-line client (Windows users: consider [Cygwin]) or a GUI of your choice. 

Required Accounts:
* [GitHub]: Web-based source code management. Account required for full access to this SDK.
* [Firebase]: Cloud database used by the SDK. Sign up for free account, no download needed. 

[AltspaceVR client]: http://account.altspacevr.com
[Firebase]: http://firebase.com
[Prepros]: https://prepros.io/
[Sublime Text Editor]: http://www.sublimetext.com/
[GitHub]: https://github.com/
[GitHub Client]: http://git-scm.com/downloads/guis
[Cygwin]: https://www.cygwin.com/
