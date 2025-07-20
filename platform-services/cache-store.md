# Cache Store

The Cache Store provides simple key/value cache storage. The Cache Store API can be accessed using `Platform.Server.CacheStore`.

* Cache Store is not durable. Data will be cleaned up if not used.
* The Cache Store API can only be used on the server.
* Cache Store is faster than Data Store.

Some common use cases for Cache Store are:

* Temporary Cooldowns on accessing content
* Share Codes for joining a match

{% hint style="info" %}
Cache Store is intended to be used for short-lived, non-durable key/value storage. If you need persistent storage without expiration times, checkout [Data Store](data-store/).
{% endhint %}

## Common Patterns

```typescript
// Create a queue cooldown
await Platform.Server.CacheStore.SetKey(
    `BossQueue:${player.userId}`, // The key for this cache entry
    os.time(), // The time the cooldown was created is stored as the value
    60, // 60 second cooldown
);

// Check a queue cooldown
const result = await Platform.server.cacheStore.GetKey<number>(`BossQueue:${player.userId}`);
if (result) {
    // On cooldown
} else {
    // Not on cooldown
}
```
