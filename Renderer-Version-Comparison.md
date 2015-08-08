There are currently two active renderer versions. 0.2.0 should be used in almost every case, but there may still be examples and meshes that render in 0.1.0 that don't work yet.

**If you are switching between renderers, you must make sure that you switch the version number, the loader type, and the number of arguments at the same time or nothing will render!**

|  | 0.2.0 | 0.1.0 |
|---|---|---|
| Renderable Objects | Most three.js Geometry | Only meshes loaded by AltOBJMTLLoader |
| OBJMTLLoader to use | OBJMTLLoader | AltOBJMTLLoader |
| Number of arguments to load() | two, the .obj file and the .mtl file | one the .obj file with the .mtl calculated by replacing the extension |
|  |  |  |
|  |  |  |
|  |  |  |