Headscratching?
===============

Here are some things that might help

1. A-Frame seems to ignore components with names containing a capital letter.
A-Frame uses a deterministic conversion from camel case (myNewComponent) to hyphenated (my-new-component) and vice versa. In HTML you always use the hyphenated version for component names and properties, but you can use either one in javascript.
So 'myNewComponent' won't work; use hyphens to separate words instead e.g. 'my-new-component'.

2. Weird property values in A-Frame. If you are writing an a-frame component and referring to object3Ds belonging to other elements within the 'init' method,
you may find that properties of the referred to object don't have the values you expect (position for instance). This is because
these other objects have not completed initialisation yet.

Like regular HTML, A-Frame entities load depth-first, top to bottom. Components load left to right in a single entity.

    <a-entity id='one'> // loads once all its children are loaded
        <a-entity id='two'> // loads once all its children are loaded
            <a-entity id='three'> // loads first
            </a-entity>
        </a-entity>
    </a-entity>

The a-scene and all other a-frame elements emit a 'loaded' event to which
you can listen and run your dependent code:
    ```javascript
    var target = document.querySelector('#target');
    if (target.hasLoaded) {
        doThis();
    } else {
        target.addEventListener('loaded', doThis);
    }
    ```

3. Beware of setting angles in degrees. Three.js uses radians for everything, but A-Frame uses degrees. So rotation='0 180 0', but this.object3D.rotation.set(0, Math.PI, 0).

4. N-sound components do not work when 'volume' property is set.

5. Creating > 1 AudioContext in javascript will cause the client to freeze. You should only need one anyway, just make sure you aren't creating more in error (or temporarily).