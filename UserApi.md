(better documentation coming soon)

Example Usage:

```
window.addEventListener("altuserenter", function( object ) {
  users[object.userId] = {firstName: object.firstName, isLocal: object.isLocal};
  console.log(object.firstName + " has entered the space.");
});

window.addEventListener("altuserleave", function( object ) {
  delete users[object.userId];
  console.log(object.firstName + " has exited the space.");
});

window.Alt.Users.getUsers().then(
  function(val) {
    val.forEach(function(user) {
      users[user.userId] = {firstName: user.firstName, isLocal: user.isLocal};
      if (user.isLocal) {
        console.log(user.firstName + " is the local user");
        localUserId = user.userId;
      }
    });
  }
);
```