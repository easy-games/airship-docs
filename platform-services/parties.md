# Parties

The Party API provides a single, platform level party system. Players can stay in the same party even if they are not in the same server or the same game. You can access party information using `Platform.server.party` and `Platform.client.party`.

* Players are always in a party when online. By default, a player will be in a party by themselves.
* A player's party can change at any time.

## Common Patterns

```typescript
// Get a user's party
const response = await Platform.party.GetPartyForUserId(player.userId);
if (!response.succes) return;
if (!response.data) {
    // No party. The user may have no party if they are offline.
}

// Party data such as members and leader
const party = response.data;
```
