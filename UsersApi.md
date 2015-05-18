(better documentation coming soon)

Example Usage:

```
window.addEventListener("altuserenter", function( user ) {
  console.log(user.displayName + " has entered the space.");
});

window.addEventListener("altuserleave", function( user ) {
  console.log(user.displayName + " has exited the space.");
});

window.Alt.Users.getLocalUser().then(function(localUser) {
    console.log(localUser.displayName + " is the local user");
});

**Currently Depreciated**

window.Alt.Users.getUsers().then(
  function(val) {
    val.forEach(function(user) {
      users[user.userId] = {displayName: user.displayName, isLocal: user.isLocal};
      if (user.isLocal) {
        console.log(user.displayName + " is the local user");
        localUserId = user.userId;
      }
    });
  }
);
```