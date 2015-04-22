### Guidelines for Contributing to the AltspaceSDK

When contributing code:
* In your [Pull Request](../pulls) comment, note the Issue that your change fixes or implements.
* If no relavent Issue, create one on the [issues page](../issues) before you begin work.  
* After adding or changing user-visible methods, update the [[SDK Reference]].
* Where possible, follow [Mr. doob's Code Style] used in the [Three.js] repo. 

Additional guidelines - based on [Three.js Contribution Guidelines]
* Create separate branches per patch or feature.
* Once done with a patch or feature, do not add more commits to a feature branch. (Pull requests are not repository state snapshots; any change you make in that branch will be included in the pull request.)
* If you add a new feature it's good to add also an example (both for showing how it's used and for testing it still works after eventual refactorings).
* If you add some assets for the examples (like textures, models, sounds, etc), make sure they have a proper license allowing for their use here. (Less restrictive is better.)  Add attribution links to the `ATTRIBUTIONS.md` file in the relevant asset directory.
* If you modify existing code (refactoring / optimization / bug fix), run relevant examples to check they didn't break or that there wasn't some performance regress.

Copyright Notice: All contributions to this repo become property of AltspaceVR.

[Mr. doob's Code Style]: https://github.com/mrdoob/three.js/wiki/Mr.doob%27s-Code-Style%E2%84%A2
[Three.js]: https://github.com/mrdoob/three.js 
[Three.js Contribution Guidelines]: https://github.com/mrdoob/three.js/wiki/How-to-contribute-to-three.js

