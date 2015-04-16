This tutorial is a more detailed walk-through of the Spinning Cube app in the SDK repo [README].

### Step 1. Create your app HTML file

First clone or [download] the [AltspaceSDK Repo] from GitHub.

You can also using a GitHub GUI, command line shown here for brevity.
```
$ git clone git@github.com:AltspaceVR/AltspaceSDK.git
```
This will create the AltspaceSDK directory, with the following files and directories.
```
$ ls AltspaceSDK
src/
lib/
examples/
README.md
README.html
```
You could start building your app in this AltspaceSDK directory.  However, we recommend you **create a copy of the SDK files for each app that you build**.  The reasons are as follow: (1) your app will be self-contained in one directory, making it easier to move or copy, and (2) your older apps can continue using an older version of the SDK.  Keep in mind this SDK is in BETA status and could change frequently, including non-backwards-compatible upgrades or discontinuing support for older versions.

For example, we create a MyFirstApp directory and copy SDK files as follows.
```
$ mkdir MyFirstApp
$ cp -r AltspaceSDK/src MyFirstApp/sdk
$ cp -r AltspaceSDK/lib MyFirstApp/lib
$ ls MyFirstApp/
lib/
sdk/
```
(If you use another directory structure, remember to adjust the paths used in your `<script>` tags below.)




[AltspaceSDK Repo]: https://github.com/AltspaceVR/AltspaceSDK
[README]: https://github.com/AltspaceVR/AltspaceSDK
[download]: https://github.com/AltspaceVR/AltspaceSDK/archive/master.zip

