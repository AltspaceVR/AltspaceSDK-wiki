Created by: NorybiaK (Kai)  
Source: [Aframe-gltf](https://github.com/norybiak/Aframe-gltf)


##About
gLTF loader component and primitive compatible with a-frame 0.3.0

## Files types
* .gltf and .glb

## Using Aframe-gltf in AltspaceVR

```javascript
<html>
  <head>
    <script src="https://aframe.io/releases/0.3.0/aframe.min.js"></script>
    <script src="https://cdn.rawgit.com/AltspaceVR/aframe-altspace-component/v1.4.0/dist/aframe-altspace-component.min.js"></script>

    <script src="https://cdn.rawgit.com/norybiak/Aframe-gltf/v0.1.1/dist/aframe-gltf.js"></script>
  </head>
  <body>

    <a-scene altspace>

      <a-gltf-model src="path/to/model.gltf"></a-gltf-model>
      
                              - OR -
                              
      <a-entity gltf-model="path/to/model.gltf"></a-entity>

    </a-scene>
    
  </body>
</html>
```
