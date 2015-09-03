This article helps you transition from our legacy renderer 0.1.0 to our new 
0.2.0 renderer. The new renderer will soon become the default for AltspaceVR 
apps.

## Instantiating the renderer

Regardless of which version you are using, you should be instantiating the
renderer via the `altspace.getThreeJSRenderer()` method. At the time of this
writing (Sept 9th), the `getThreeJSRenderer` method will return renderer 
0.1.0 by default, if you do not specify a version. However, it is recommended
that you explicitly specify a version because the default _will_ change in 
the coming weeks. Simply use an options argument to specify a version:

    altspace.getThreeJSRenderer({version: '0.1.0'});

## What's new in 0.2.0

Renderer 0.1.0 restricted you to OBJ/MTL files, which you _had_ to load through
the AltOBJMTLLoader. Renderer 0.1.0 removes this restriction and allows you to
use any method of importing or creating geometry and textures that Three.js
supports. This means that you can now use Three.js' primitive geometries,
such as BoxGeometry, CylinderGeometry, SphereGeometry, etc to create 3D objects.

You can also use any of the formats and loaders supported by Three.js, such as
OBJMTLLoader, ColladaLoader, DDSLoader, STLLoader, etc, including animations.

Since AltspaceVR uses unlit environments, you are still limited to 
MeshBasicMaterial however, the new renderer also supports material `color` and 
visibility, via the `visible` property. 


## Caveats and unsupported features

Renderer 0.2.0 is still in development so there are known bugs at the time of
this writing. These bugs include:

- Incorrect UV mapping - textures appear stretched or flipped on some surfaces
- Decreased performance on scene loading and scene updates
- Inverted geometry - geometry appears flipped across the X axis

We are working on fixing these issues as soon as possible.

Additionally, renderer 0.2.0 does not support all features of Three.js materials
and meshes at the time of this writing, such as:

- Material transparency
- MeshBasicMaterial alphaMap
- MeshBasicMaterial wireframe
- Dynamic textures
- Dynamic geometry
- Animated SkinnedMeshes
