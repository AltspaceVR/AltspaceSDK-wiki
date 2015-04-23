This page describes the typical workflow for developing an Altspace Web App.

## Workflow Overview

When building an app from scratch, we recommend developing it inside of Altspace. It is possible to use a normal WebGL renderer when your app detects that it is not in Altspace, and develop in chrome, but things may render differently.

While developing in Altspace, it can be helpful to have the client in 2D windowed mode. To do this, start Altspace with your Oculus unplugged or turned off which should cause it to launch in 2D mode. Then either hold shift before Altspace loads (after logging in) and pick windowed mode, or use the windowed-mode toggle shortcut when Altspace is running: **left-command (OSX) / left-ctrl (Win) + left-alt + W** (on Windows... known issue: the Altspace window may go blank/blue when switching to windowed mode, just use the shortcut twice more to toggle to full-screen then back again.)  You now should also be able to drag the far edges of the window to resize it, even if the resize cursor does not appear. You may also want to not have Altspace lock your cursor when clicking on the window (to move the title bar for example). This can be toggled via **left-command (OSX) / left-ctrl (Win) + left-alt + C**.

It is also extremely helpful to use a local webserver that supports live-reload. We recommend Prepros. Developing from file:// is not recommended due to cross domain issues.

## Requirements Overview

Hardware Requirements
* Oculus Rift DK2 (for VR mode; developing in non-VR mode also supported)
* Windows or Mac laptop or desktop computer
  * lastest version of OS (Windows 8.1, OS X Yosemite) recommended
* Dedicated GPU (for high-performance graphics)

Note the above requirements are for developing Altspace apps, not for simply running Altspace, which can be done on computers without a dedicated GPU.  The additional graphics power is needed when developing apps since you will also be running additional debugging tools, described below. (Integrated graphics *may* work, although not officially supported.)

Some hardware platforms successfully used for building Altspace Apps:
* Custom Gaming Desktop (i7/R9 200)
* Asus ROG G751 17" laptop (i7/GTX 980M)
* Lenovo Y50 15" laptop (i7/GTX 860M)
* Alienware 13" laptop (i5/GTX 860M)
* Macbook Pro 15" laptop (i7/GT 750M)

Recommended Software:
* [AltspaceVR client]: executable; access to Altspace client source code is not required.
* [Prepros]: Web dev tool with integrated web server and automatically page reloading.
* [Sublime Text Editor]: Recommended; use any editor or IDE that supports Javascript.
* Coherent Debugger: Allows you to see the console output of your Altspace web app
    * [OSX Debugger]
    * [Windows Debugger]
    * on Mac: cannot rename it from Debugger.app after you extract it, or it won't run
    * due to legacy .app bundle structure -- it needs an Info.plist with metadata.
* [GitHub Client]: any command-line (Windows users: consider [Cygwin]) or a GUI client. 

Required Accounts:
* [GitHub]: Web-based version control. Account required for access to this SDK.

Recommended Accounts:
* [Firebase]: Cloud synchronization service useful for Altspace apps.

[AltspaceVR client]: http://account.altspacevr.com
[Firebase]: http://firebase.com
[Prepros]: https://prepros.io/
[Sublime Text Editor]: http://www.sublimetext.com/
[GitHub]: https://github.com/
[GitHub Client]: http://git-scm.com/downloads/guis
[Cygwin]: https://www.cygwin.com/
[OSX Debugger]: http://sdk.altvr.com/debugger/DebuggerMacOSX.zip
[Windows Debugger]: http://sdk.altvr.com/debugger/DebuggerWindows.zip
