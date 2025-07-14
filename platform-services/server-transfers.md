# Server Transfers

The transfer APIs allow you to move players between servers. You can access server transfer functions using `Platform.Server.Transfer`.

```typescript
// Allocate a new server. The default acess mode is Closed. This server
// will only be accessible to players moved via server side transfer requests.
const server = await Platform.Server.ServerManager.CreateServer({
    sceneId: "CustomScene",
});
// Move players to the new server.
await Platform.Server.Transfer.TransferGroupToServer(players, server.serverId);
```

## Transfer Functions

### Transfer to Game

Transfers a group of players to the given game, additionally you can provide a preferred server ID. This preferred server ID can be on any scene. Access checks will be applied for all players. If any players cannot be transferred to the preferred server, a default server will be found or created and all players will be transferred there.&#x20;

{% hint style="info" %}
See the [#access-modes](server-transfers.md#access-modes "mention") section for more information on how server access is decided.
{% endhint %}

### Transfer to Matching Server

This function uses the parameters you provide to find a game server for a group of players. This function does _not_ check that players are allowed to access the matching server. If you want to use access checks, use the "TransferToServer" function.

This function is useful for cases where you already know access is allowed, or you explicitly want to ignore access rules.

### Transfer to Server

This function allows you to transfer a group of players to a specific server ID. If any players are unable to access the provided server ID, the function will fail. If you want to ignore access checks, use the "TransferToMatchingServer" function instead.

### Transfer to Player

Transfers a group of players to a target player. If any of the players are unable to access the server the target player is on, the players without access will be left behind and remain in their current server.

### Common Behaviors

There are a few common behaviors for all transfer functions:

* A player can only be transferred by a game server if the player is currently playing that game.
* Any game server can transfer any player playing the game.
* Transfers are not guaranteed. It is possible for the client to cancel or ignore the transfer request. The success value returned by the API only indicates that the transfer request was submitted, not that the transfer has occurred.
* Generally transfers happen almost instantly, but it is possible for a transfer to occur after a few minutes depending on server availability and startup time.

## Starting Scenes

When a server is created, a starting scene is provided to the server. This starting scene is recorded for the lifetime of the server, and is used when deciding how to route players to a server. If the server changes its scene while running, server selection and transfer behavior will not be affected and the starting scene will continue to be used.

{% hint style="info" %}
To change the default starting scene, you can modify  "Starting Scene" in the `GameConfig` asset.
{% endhint %}

<table><thead><tr><th width="315">Transfer Function</th><th>Scene Awareness</th></tr></thead><tbody><tr><td><code>TransferToServer()</code> </td><td>Ignores the server starting scene entirely. Players are always moved to the server if access is allowed.</td></tr><tr><td><code>TransferToGame()</code> </td><td>Will first attempt to transfer the players to the preferred server first, this attempt does <em>not</em> check the starting scene. If the preferred server cannot be joined, a server on the default scene is found or created instead.</td></tr><tr><td><code>TransferToMatchingServer()</code></td><td>Matches the starting scene provided in the configuration parameters. If no sceneId is provided, any scene will be accepted.</td></tr><tr><td><code>TransferToPlayer()</code></td><td>Ignores the server starting scene entirely. Players are always moved to the server if access is allowed.</td></tr></tbody></table>

## Access Modes

All game servers are assigned an access mode when they are created. Access modes control which players can join a given game server and the methods by which they can join the server. Default servers a client joins through the main menu will always have the "Open" access mode. You can create servers with different access modes using the `CreateServer` function.

{% hint style="info" %}
Access Mode can be changed at runtime using the Server Manager API: `Platform.Server.ServerManager.SetAccessMode();`
{% endhint %}

<table><thead><tr><th width="198">Access Mode</th><th>Description</th></tr></thead><tbody><tr><td>Open</td><td>Any player is allowed to join the server.</td></tr><tr><td>Closed</td><td>Clients cannot join the server through their friends list or client side transfer requests. Players can only join if a game server requests the transfer. This is the default mode for new servers created with <code>CreateServer()</code></td></tr><tr><td>Friends Only</td><td>Only users that have friends on the server can join. Server side transfer requests will also respect this mode. This means that the first player to join the server must be transferred using TransferToMatchingServer (see examples below).</td></tr></tbody></table>

## Transfer Data

When transferring a player or group of players, you can optionally specify a few configuration fields:

<table><thead><tr><th width="263">Field</th><th>Description</th></tr></thead><tbody><tr><td><code>clientTransferData</code></td><td>An object that will be passed to the client. This is also visible to the server they join.</td></tr><tr><td><code>serverTransferData</code></td><td>An object that will be passed to the game server when the client joins. This is not visible to the client.</td></tr><tr><td><code>loadingScreenImageId</code></td><td>The ID of the image to display on the loading screen for this transfer. You can upload loading screen images on the<a href="https://create.airship.gg/dashboard/organization/game/settings"> Airship Create</a> site.</td></tr></tbody></table>

## Common Patterns

### Transfer Players to Default Servers

```typescript
// Transfer players back to your game's lobby (Default servers)
await Platform.Server.Transfer.TransferGroupToGame(players, Game.gameId);
```

### Create a Match Server Anyone Can Join

```typescript
// Create an open match server. Anyone can join these servers at any time.
let server = await Platform.Server.ServerManager.CreateServer({
    accessMode: AirshipServerAccessMode.Open, // The default mode is Closed
    sceneId: "MatchScene",
});
await Platform.Server.Transfer.TransferGroupToServer(players, server.serverId);
```

```typescript
// Backfill a group to an open match server in their region.
await Platform.Server.Transfer.TransferGroupToMatchingServer(players, {
    sceneId: "MatchScene",
    accessMode: AirshipServerAccessMode.Open,
});
```

### Find or Create a Server

```typescript
// Find a server for the group. Make sure we check that the access mode is set to
// "Open" so we don't accidently join a private match.
const result = await Platform.Server.Transfer.TransferGroupToMatchingServer(players, {
    sceneId: "MatchScene",
    accessMode: AirshipServerAccessMode.Open,
})
// "transfersRequested" being true means the group found a server, so we are done.
if (result.transfersRequested) return;

// Create a new server for the group and transfer them to it.
const server = await Platform.Server.ServerManager.CreateServer({
    sceneId: "MatchScene",
    // Access mode is Closed by default, so we set it to open explicitly
    accessMode: AirshipServerAccessMode.Open,
});
await Platform.Server.Transfer.TransferGroupToServer(players, server.serverId);
```

### Create a Private Match

```typescript
// Create a private match server for a group
const server = await Platform.Server.ServerManager.CreateServer({
    sceneId: "MatchScene",
    // We can use any access mode in combination with allowedPlayers. Players must
    // pass the checks for both access mode and be on the allowed players list
    // to join the server.
    accessMode: AirshipServerAccessMode.Closed,
    allowedPlayers: players,
});
await Platform.Server.Transfer.TransferGroupToServer(players, server.serverId);
```

### Transfer to Another Player

```typescript
// Transfer a group to a player in another server.
const result = await Platform.Server.Transfer.TransferGroupToPlayer(
    players,
    targetUserId
);

// We can check the result to see which players were transferred
if (result.transfersRequested) {
    print("These users were transferred:", inspect(result.userIds));
}
```

### Create a Friends Only Match

```typescript
// Create a server that only friends can join
const server = await Platform.Server.ServerManager.CreateServer({
    sceneId: "MatchScane",
    accessMode: AirshipServerAccessMode.FriendsOnly
});

// Transfer the owner of the match using TranferToMatchingServer
await Platform.Server.Transfer.TransferToMatchingServer(player, {
    serverId: server.serverId,
});
```

```typescript
// Other players can join using any of these methods:
await Platform.Server.Transfer.TransferToGame(otherPlayer, Game.gameId, serverId);
await Platform.Server.Transfer.TransferToPlayer(otherPlayer, friendUserId);
await Platform.Server.Transfer.TransferToServer(otherPlayer, serverId);

// You could also send anyone to the server using the TransferToMatchingServer
// function. Keep in mind, this does not perform any access checks.
await Platform.Server.Transfer.TransferToMatchingServer(otherPlayer, {
    serverId: server.serverId
})
```
