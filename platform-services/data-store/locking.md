# Locking

Data Store keys can be locked to a specific game server by calling `LockKeyOrStealSafely()` or `LockKey()`. Keys can be locked in two modes:

| Mode        | Description                                                                   |
| ----------- | ----------------------------------------------------------------------------- |
| `ReadWrite` | Blocks reads and writes on all other servers. This is the default.            |
| `Write`     | Blocks writes on all other servers. All servers can read the key at any time. |

A key lock will last for 24 hours, or until it is unlocked with the `UnlockKey()` function. Normally, only the server that owns the lock can unlock the key. However, other servers can steal a lock by passing the serverId that owns the lock to the `LockKey()` or `UnlockKey()` functions. This should only be done in cases where you know the lock can be stolen safely (ex. the server that owns the lock is offline). You can retrieve the current owner of a lock, along with additional lock data using `GetLockDataForKey()`.&#x20;

## Locking Patterns

For simple lock cases, it is best to use the `LockKeyOrStealSafely()` function:

```typescript
Airship.Players.onPlayerJoined.Connect(async (player) => {
	const result = await Platform.Server.DataStore.LockKeyOrStealSafely(
		`progress:${player.userId}`
	);
	if (!result) player.Kick("Unable to load progress.");
	
	// You can now safely read and write to this key. No other server
	// can read or modify it.
	this.progress[player.userId] = await Platform.Server.DataStore.GetKey(
		`progress:${player.userId}`
	);
});

Airship.Players.onPlayerDisconnected.Connect(async (player) => {
	await Platform.Server.DataStore.SetKey(
		`progress:${player.userId}`,
		this.progress[player.userId],
	);
	delete this.progress[player.userId];
	// Release the key when the player disconnects.
	await Platform.Server.DataStore.UnlockKey(`progress:${player.userId}`);
});

Platform.Server.Transfer.onShutdown.Connect(() => {
	Promise.allSettled(ObjectUtils.keys(this.progress).map(async userId => {
		await Platform.Server.DataStore.SetKey(
			`progress:${player.userId}`,
			this.progress[player.userId],
		);
		await Platform.Server.DataStore.UnlockKey(
			`progress:${player.userId}`
		);
	})).expect();
});
```
