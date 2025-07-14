# Server List

Airship provides a basic server list that can be used to retrieve servers which may be accessible to a player in your game. The server list functions can be found in `Platform.Server.ServerManager`.

## Listing a Server

A server can be listed at any time using the following code:

```typescript
await Platform.Server.ServerManager.ListServer({
    // Name and description are optional
    name: "My Server",
    description: "A running server you can join",
})
```

You can call this again to update the name or description.

## Delist a Server

If you want to remove a server from the list, you can do so at any time using the following code:

```typescript
await Platform.Server.ServerManager.DelistServer();
```

Calling this function multiple times will have no effect.

## Retrieving the Server List

The server list for a game can be retrieved on both the client and server side. Both the client and server have access to the full list using `GetServerList()`. This function returns the most populated servers first.

Additionally, the client has access to `GetFriendServers()` which returns any listed servers their friends are playing on.

## Common Patterns

### Create a Match with a Lobby Only Friends Can Join

```typescript
// When the player clicks "create a lobby", create a server for them and move them
// to it.
const server = await Platform.ServerManager.CreateServer({
    sceneId: "LobbyScene",
    accessMode: AccessMode.FriendsOnly,
});
// We use "TransferToMatchingServer" to bypass the access rules for the owner. We
// won't do this for other players since we want to perform access checks for them.
await Platform.Server.Transfer.TransferToMatchingServer(player, {
    serverId: server.serverId,
});
```

```typescript
// In our lobby scene on the new server, we can list the server when a player joins
const cleanUpConnection = Airship.Players.onPlayerJoined.Connect(async (player) => {
    // The first player to connect is the owner of the lobby
    owner = player;
    // Clean up the connection so we don't overwrite the owner when another
    // player joins
    cleanUpConnection();
    
    // List the server for the owner's friends to find
    await Platform.Server.ServerManager.ListServer({
        name: `${owner.username}'s Server`
    })
})

// We can also unlist the server when the owner starts the match
YourGameManager.onStartMatch.Connect(async () => {
    await Platform.Server.ServerManager.UnlistServer();
})
```

```typescript
// Clients can retrieve servers their friends are on
const servers = await Platform.Client.ServerList.GetFriendServers();

// When they select their friend's lobby in a UI, send a network request to the
// server they are connected to requesting to transfer. (You'll have to set this up,
// see our docs on Network Functions)
Network.JoinLobby.client.FireServer(server.serverId);
```

```typescript
// On the friends server, we get the client event and process it
Network.JoinLobby.server.OnClientEvent((player, serverId) => {
    // We can get the requested server's data to do additional checks
    // if we want to.
    const serverData = await Platform.Server.ServerManager.GetServer(serverId);
    if (!serverData || serverData.sceneId !== "LobbyScene") return;
    
    // Send the friend to the new lobby server
    await Platform.Server.Transfer.TransferToServer(friend, serverId);
})
```
