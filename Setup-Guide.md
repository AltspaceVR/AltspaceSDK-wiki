>_We find this the easiest way to develop VR web apps for AltspaceVR, but feel free to substitute other tools or experiment with developing in VR mode. You can also skip the AltspaceVR step if you would rather develop using WebGL in a traditional web browser._

###Configure AltspaceVR
1. Launch and login to AltspaceVR without an HMD connected
2. After the program is running, switch AltspaceVR into windowed mode  
 OSX: <kbd>Left Command</kbd>+<kbd>Left ALT</kbd>+<kbd>W</kbd>  
 Win: <kbd>Left CTRL</kbd>+<kbd>Left ALT</kbd>+<kbd>W</kbd>  
3. Move or snap the window to right side of your monitor  
 Win: <kbd>Windows</kbd> + <kbd>Right Arrow</kbd>

  >Windows: If the window remains black, you may need to snap or resize it a couple times for an image to appear  

###Setup Coding Environment
1. Checkout (or download and unzip) this repo to your project folder
2. Download and run [Sublime Text]
3. Drag your project folder into Sublime
4. Move or snap Sublime to left side of your monitor  
 Win: <kbd>Windows</kbd> + <kbd>Left Arrow</kbd>
5. Download and run [Prepros]  

   >Developing from file:// is not recommended due to cross domain issues.
6. Drag your project folder into Prepros

###Test Example
1. Hit preview in Prepros, navigate to an example, and copy the URL
2. Switch to AltspaceVR, open up the Apps panel, and paste it into the URL bar

  >Using the Apps panel is recommended as it has the same dimensions as all the public enclosures in AltspaceVR so you do not need to currently worry about your holographic application needing to be responsive to changes in pixel dimension.
3. Make a few modifications to the example in Sublime.  
Every time you save the file, your changes should immediately appear in AltspaceVR (this is via a LiveReload script added by Prepros).

###Test Debugger
1. Download the Coherent Debugger, which is essentially a remote Chrome inspector for AltspaceVR.  
 OSX: [OSX Debugger]  
 Win: [Windows Debugger]

 > OSX: Note that you cannot rename it from Debugger.app after you extract it, or it won't run due to legacy .app bundle structure -- it needs an Info.plist with metadata.  
2. Run the debugger and click `GO`
3. Find your test example in the list

[OSX Debugger]: http://sdk.altvr.com/debugger/DebuggerMacOSX.zip
[Windows Debugger]: http://sdk.altvr.com/debugger/DebuggerWindows.zip

[Sublime Text]: http://www.sublimetext.com/
[Prepros]: https://prepros.io/