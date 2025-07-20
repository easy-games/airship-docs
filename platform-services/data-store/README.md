# Data Store

The Data Store provides simple key/value persistent storage. The Data Store API can be accessed using `Platform.Server.DataStore`.

* Data Store is durable. Data saved will not be deleted or cleaned up.
* The Data Store API can only be used on the server.
* Data Store is slower than Cache Store.

Some common use cases for the Data Store are:

* User Profiles
* Tracking Unlocks
* Persistent Inventory

{% hint style="info" %}
Data Store is intended to be used for general purpose persistent key/value storage. Check out [Cache Store](../cache-store.md), [Leaderboards](../leaderboards.md), and [Platform Inventory](../platform-inventory.md) for more specialized data storage situations.
{% endhint %}

{% hint style="info" %}
Data store keys must be alphanumeric and only contain allowed symbols: -, ., \_, :
{% endhint %}

## Common Patterns

```typescript
// Store user unlocks
const unlocks: UnlockData = {
    level1: true,
    level2: true,
    level3: false,
}
await Platform.Server.DataStore.SetKey(`Unlocks:${player.userId}`, unlocks);

// Get user unlocks
const result = await Platform.Server.DataStore.GetKey<UnlockData>(
    `Unlocks:${player.userId}`,
);
if (!result) return; // Key did not exist

// Check if user has unlocked level2
if (result.level2) {
    // Unlocked!
}
```
