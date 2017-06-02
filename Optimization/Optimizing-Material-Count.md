Material instances lead to additional draw calls when rendering your app.
Re-use material instances as much as possible. Avoid cloning or duplicating materials if they share properties that never change.
In some instances, material re-use can lead to further optimizations thanks to render batching, where objects with the same 
material are 
Use texture atlasing with texture offsets where possible. 
This would allow you to use a single material to represent different objects.
