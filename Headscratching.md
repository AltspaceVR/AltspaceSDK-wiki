Headscratching?
===============

Here are some things that might help

1. A-Frame ignores components with names containing a capital letter.
It's true, if you give your a-frame component a name containing a capital letter a-frame won't load it, or give you any error (A-Frame 0.3.0).
So 'myNewComponent' won't work. Use hyphens to separate words instead e.g. 'my-new-component'.

2. Weird property values in A-Frame. If you are writing an a-frame component and referring to object3Ds belonging to other elements within the 'init' method,
you may find that properties of the referred to object don't have the values you expect (position for instance). This is because
these other objects have not completed initialisation yet. The a-scene and all other a-frame elements emit a 'loaded' event to which
you can listen and run your dependent code:
    ```javascript
    var target = document.querySelector('#target');
    if (target.hasLoaded) {
        doThis();
    } else {
        target.addEventListener('loaded', doThis);
    }
    ```
3. Beware of setting angles in degrees. APIs generally assume radians (is this true)?

4. N-sound components do not work when 'volume' property is set.