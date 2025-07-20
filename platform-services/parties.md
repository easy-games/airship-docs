# Parties

The Party API provides a single, platform level party system. Players can stay in the same party even if they are not in the same server or the same game. You can access party information using `Platform.Server.Party` and `Platform.Client.Party`. You can invite or remove players from a party in `Platform.Client.Party`.

* Players are always in a party when online. By default, a player will be in a party by themselves.
* A player's party can change at any time.

{% hint style="info" %}
If you're looking to create your own party or group system in a game, checkout [Matchmaking Groups](matchmaking.md#groups). Matchmaking groups gives your game full control over how players are grouped and can be used even if you don't need matchmaking services.
{% endhint %}

## Common Patterns

```typescript
// Get a user's party
const party = await Platform.party.GetPartyForUserId(player.userId);
if (!party) return; // No party. The user may have no party if they are offline.

// Party data such as members and leader
const members = party.members;
```
