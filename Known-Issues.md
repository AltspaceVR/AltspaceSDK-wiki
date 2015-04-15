## Limitations of Altspace Browser
* based on **Chromium 28** ([latest version][1] is 44 as of 4/14/2015)
* new tabs / pages not supported
* cannot print / download
* 3D CSS not suported well
* Audio: no mp3 (unlike Chrome).  List of [Supported Media formats][2].
    * Please use only webaudio, if you use flash we will cry.
    * Your audio will sound like it is coming from the middle of your webpage.
    * In future releases: specialized audio elements for positional sound.
* Traditional DOM is only in a single plane right now, cannot be put on 3d objects.

## Limitations of Three.js Support
* Cannot import Three.js scenes or lighting, animations, or cameras
* No dynamic or modified meshes, dynamic or modified materials, or custom shaders.
* No screen space effects, point clouds, or particle effects, or other tricky stuff.
* Cannot hide objects once added to the scene, or have transparent objects.


[1]: https://chromium.googlesource.com/chromiumos/manifest-versions/+/master/paladin/buildspecs/
[2]: https://developer.mozilla.org/en-US/docs/Web/HTML/Supported_media_formats