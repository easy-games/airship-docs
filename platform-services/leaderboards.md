# Leaderboards

The Leaderboard API can be accessed using `Platform.server.leaderboard`.

* Leaderboards are durable. Data will not be cleaned up or deleted.
* The Leaderboard API can only be used on the server.
* Overall leaderboard rankings retrieved from GetRankRange() will reflect changes immediately.
* Placement for individual entries retrieved from GetRank() may take up to 1 minute to reflect changes.

Leaderboards must be created on the create dashboard before use:

[https://create.airship.gg/dashboard/organization/game/leaderboards](https://create.airship.gg/dashboard/organization/game/leaderboards)

## Leaderboard Keys

If you are tracking player stats with leaderboards, it's often best to use the player's userId as the key. Though the most common keys are user IDs, you can use any unique value as a leaderboard key. For example, if you have a clan system in your game, you could use the clan ID to track total wins for a given clan.

## Common Patterns

```typescript
// Update a leaderboard
await Platform.server.leaderboard.Update("TopScores", {
    [player1.userId]: 123,
    [player2.userId]: 234,
})
```

```typescript
// Get top scores for a leaderboard in realtime
const result = await Platform.server.leaderboard.GetRankRange("TopScores");
if (!result.success) return;

// Contains an array of objects with the id, rank, and value
const entries = result.data;

// Get the usernames to display
const userResult = await Platform.server.user.GetUsersById(entries.map(e => e.id));
if (!userResult.success) return;
const idMap = userResult.data;

// Array of objects containing userData, rank, and scoreValue.
const entriesWithUserdata = entries.map((entry) => {
    return {
        username: idMap[entry.id]?.username ?? "Unknown User",
        rank: entry.rank,
        scoreValue: entry.value,
    }
});
```

```typescript
// Get the rank of a given id (note: results may be delayed up to 1 minute)
const result = await Platform.server.leaderboard.GetRank("TopScores", player.userId);
if (!result.success) return;

// Contains an object with the id, rank, and value
const entry = result.data;
```
