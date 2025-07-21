---
description: Matchmaking Platform Documentation
---

# Matchmaking

## Overview

The Airship platform provides a robust Matchmaking system for game developers to quickly implement competitive, multiplayer gaming. With minimal configuration, you can easily setup skill based, role based, and other types of matchmaking queues that easily integrate into your existing Airship games.

## Quickstart

**More documentation is below**, this exists to help you quickly get familiar with the core concepts of matchmaking.

After creating a matchmaking queue in the Create Airship console:

```typescript
// Server
// Create a matchmaking group with various users
const createGroupResult = await Platform.Server.Matchmaking.CreateGroup(
    userIds,
);
const groupId = createGroupResult.groupId;
```

```typescript
// Join a preconfigured matchmaking queue
// This begins the matchmaking process for this group
// Configure your matchmaking queue's on create.airship.gg
await Platform.Server.Matchmaking.JoinQueue({
    groupId: groupId,
    queueId: "team-deathmatch", 
});
```

```typescript
// Leave a matchmaking queue
await Platform.Server.Matchmaking.LeaveQueue(this.matchmakerSingleton.groupId);
```

```typescript
// Leave the matchmaking process on a game client, setting the matchmaking group
// to IDLE.
// Note: The user will still be a part of the group and the entire group will leave
// the queue.
// To start matchmaking again, the server will need to call
// `Platform.Server.Matchmaking.JoinQueue`
const result = await Platform.Client.Matchmaking.LeaveQueue();
```

```typescript
// Get information about groups and their status

// Server

// Get matchmaking group + status
const group = await Platform.Server.Matchmaking.GetGroupById(
    this.matchmakerSingleton.groupId,
);

// Get the matchmaking group + status for a specific user
// This is useful if you don't have the group id, check if they are in a group
const group = await Platform.Server.Matchmaking.GetGroupByUserId(
    player.userId,
);

// On a server that was started by the matchmaking service, you can get
// the match configuration, which includes the teams, groups, players, and
// attributes for the match.
const matchConfig = await Platform.Server.Matchmaking.GetMatchConfig();

// Client

// On the player, check to see if the player is a part of a matchmaking group
const group = await Platform.Client.Matchmaking.GetCurrentGroup();

// Run code when the local player's group changes. 
Platform.Client.Matchmaking.onGroupChange.Connect((group) => {
    // This code runs when the local players group changes.
    // The "group" parameter will contain the new group data.
    print(group.status);
})
```

## Concepts

Group - A collection of players who should get put into matches together. This can be a party, a single player, or any collection of Airship Users.

Queue - Where groups get matched together. A queue has a configuration consisting of teams & rules that designate how players should be matched together.

Team - A set of Groups that are a part of a specific team in a match. Each queue must have at least one team.

Rules - Specifies how groups should be placed into teams and matches. Rules have different effects, such as requiring a minimum difference between specific attributes (eg. skill level)., specifying what roles a user can be, or the minimum difference in team size. Each queue can be configured with multiple rules to create complex matchmaking requirements.

## Groups

Groups are an immutable collection of players associated with a specific games. Players can be a part of only one group at a time and are automatically removed from previous groups when added to a new group. Groups with zero players are automatically deleted. While groups primarily exist to power matchmaking, they can also be used for other purposes, such as a simple in-game party system. (Airship already has a global party system, more info [here](parties.md)).&#x20;

A group can have one of 3 states:&#x20;

| Status     | Description                                                                                                                                       |
| ---------- | ------------------------------------------------------------------------------------------------------------------------------------------------- |
| `IDLE`     | No action is being performed. The group is in an idle state.                                                                                      |
| `IN_QUEUE` | The group is currently in a queue and waiting for a match.                                                                                        |
| `IN_MATCH` | The group is currently assigned to a match. Players in the group are expected to be in their assigned match server until the match server closes. |

A group can be in only one queue at a time and will remain in that queue until either a match is made or the request expires (about 30 minutes). To join another queue, you will either need to call `Leave Queue` or create a new group.

Players are allowed to be part of a group even if they are not playing the game. Members that are not in the game will have their "active" value set to false. If any players in the group are inactive, the group will be unable to matchmake. If a group member becomes inactive while their group is in queue, the group will automatically leave the queue.

## Queues

Queues are a collection of configuration that can be used to define a specific game mode or other concept that players can matchmake for. Each queue is separate and groups can only be part of one queue at a time.

Queues can be created on the [Create website](https://create.airship.gg). You must create a queue configuration to use Matchmaking.

## Teams

The team configuration for a queue determines the number of teams the queue has, as well as the minimum and maximum number of players for each team. Teams can be used to represent traditional two team games (Red vs. Blue team) or can represent other game modes such as Battle Royal (25 teams of 4), or asymmetric teams (one vs many). You must always have at least one team.

Each team defined in the configuration is created by selecting groups waiting in the queue. A group will never be split between teams. Keep this in mind, as groups larger than the max size for teams in a queue will not be able to find matches.

## Rules

### Difference Rule

Specifies a maximum difference between groups either at a match level (all groups) or a team level.



<table><thead><tr><th width="229">Field</th><th>Description</th></tr></thead><tbody><tr><td><strong>Attribute</strong></td><td>The attribute to compare. This can be any attribute that is present on the matchmaking group specified when joining the queue.</td></tr><tr><td><strong>Difference</strong></td><td>Maximum difference that can exist between groups for the specified group attribute.</td></tr><tr><td><strong>Scope</strong></td><td>The scope of the rule. "Match" will compare the differences for all groups in the match. "Team" will compare the differences for groups within the same team.</td></tr><tr><td><strong>Seconds Until Optional</strong></td><td>The amount of time in seconds until this rule no longer applies. Use this to loosen rule restrictions.</td></tr></tbody></table>

#### Example: Skill Based Matchmaking

Assuming a DifferenceRule with attribute set to "skill".

```typescript
// Specify the skill attribute at the group level
Platform.Server.Matchmaking.JoinQueue({
    groupId: groupId,
    queueId: "my-skill-based-queue",
    attributes: {
        "skill": 1234
    }
}).await();
```

```typescript
// If you have multiple players each with their own skill you will need to aggregate
// the skill values into one value (such as taking the average)

const numPlayers = users.length; // Assuming users already exist
const totalSkill = users.reduce((user, acc) => user.skill + acc, 0);
const avgSkill = totalSkill / numPlayers;
await Platform.Server.Matchmaking.JoinQueue({
    groupId: groupId,
    queueId: "my-skill-based-queue",
    attributes: {
        "skill": avg_skill
    }
});
```

### Match Set Rule

Compares sets of values looking for a minimum number of similarities. Useful for findings groups that share: favorite maps, purchased content, game modes, etc.

<table><thead><tr><th width="224">Field</th><th>Description</th></tr></thead><tbody><tr><td><strong>Attribute</strong></td><td>The attribute to compare. This can be any attribute containing an array of strings that is present on the matchmaking group specified when joining the queue.</td></tr><tr><td><strong>Minimum Size</strong></td><td>Minimum number of elements required to be matching between groups (set intersection). </td></tr><tr><td><strong>Seconds Until Optional</strong></td><td>The amount of time in seconds until this rule no longer applies. Use this to loosen rule restrictions.</td></tr></tbody></table>

#### Example: Selected Map Modes

Assuming a MatchSetRule with attribute set to "favoriteMaps" and difference set to 1.

```typescript
await Platform.Server.Matchmaking.JoinQueue({
    groupId: groupId,
    queueId: "my-favorite-map-queue",
    attributes: {
        "favoriteMaps": ["dust2", "rust", "strike-at-karkand"]
    }
});
```

### String Equality

Requires that all groups in the specified scope (match or team) have the same value for an attribute. With scope = match, this is useful for restricting a match to a certain type of player (eg. diamond rank)\
With scope = team, this is useful for clan based matchmaking, location vs. location, etc.&#x20;

<table><thead><tr><th width="224">Field</th><th>Description</th></tr></thead><tbody><tr><td><strong>Attribute</strong></td><td>The attribute to compare. This can be any attribute containing a string that is present on the matchmaking group specified when joining the queue.</td></tr><tr><td><strong>Minimum Size</strong></td><td>Minimum number of elements required to be matching between groups (set intersection). </td></tr><tr><td><strong>Scope</strong></td><td>The scope of the rule. "Match" will require equality for all groups in a match. "Team" will require equality for all groups on a specific team, other teams may have different values (can be required to be different with the property <code>Other Teams Should Be Different</code>)</td></tr><tr><td><strong>Other Teams Should Be Different</strong></td><td>When Scope = Team, used to require that no teams in a match share the same team equality value. This is useful for clan based matchmaking where you want Clan A vs. Clan B and want to ensure A and B are not the same value.</td></tr><tr><td><strong>Seconds Until Optional</strong></td><td>The amount of time in seconds until this rule no longer applies. Use this to loosen rule restrictions.</td></tr></tbody></table>

#### Example: Clan Based Matchmaking

Assuming a StringEquality rule with attribute set to "clan", scope set to "team" and other teams should be different set to true:

```typescript
await Platform.Server.Matchmaking.JoinQueue({
    groupId: groupId,
    queueId: "clan-4v4",
    attributes: {
        "clan": "fightingFrogs"
    }
});
```

### Team Fixed Roles

Requires each player on a team be assigned a role. Useful in role based game modes. Players can be automatically assigned a role if none is specified with the property `Automatically Assign Roles`

<table><thead><tr><th width="224">Field</th><th>Description</th></tr></thead><tbody><tr><td><strong>Teams</strong></td><td>The teams that this rule applies to.</td></tr><tr><td><strong>Attribute</strong></td><td>The attribute where the role will be specified. This can be any attribute containing a string that is present on the matchmaking <code>Player</code> specified when joining the queue.</td></tr><tr><td><strong>Match Roles</strong></td><td>Name: The name of the role that will be present for a player "dps", "healer", etc. <br>Quantity: The number of this role that should be present for a team.</td></tr><tr><td><strong>Automatically Assign Roles</strong></td><td>When a player doesn't already have a role assigned, automatically assign them a role based on whatever roles are not already filled. This can be useful if some players haven't selected the role they want to play or if you want the matchmaker to automatically assign roles to players.</td></tr><tr><td><strong>Seconds Until Optional</strong></td><td>The amount of time in seconds until this rule no longer applies. Use this to loosen rule restrictions.</td></tr></tbody></table>

#### Example: Role Based Matches

Assuming a TeamFixedRoles Rule with Attribute set to "role", match roles set to dps: 1, healer: 1, and `Automatically Assign Roles` checked.

```typescript
await Platform.Server.Matchmaking.JoinQueue({
    groupId: groupId,
    queueId: "clan-4v4",
    members: [
        {
            "uid": user1,
            "attributes": {
                "role": "dps"
            },
        }
    ]
});
```

### Team Size Balance

Used to limit the difference between team sizes in a match. Since teams can have variable minimum and maximum sizes based on expansion rules, this rule prevents creating matches where the size difference between the teams in a match is too large.

<table><thead><tr><th width="224">Field</th><th>Description</th></tr></thead><tbody><tr><td><strong>Difference</strong></td><td>The maximum size difference between two teams.</td></tr><tr><td><strong>Seconds Until Optional</strong></td><td>The amount of time in seconds until this rule no longer applies. Use this to loosen rule restrictions.</td></tr></tbody></table>

No attributes are specified at a group / player level for this rule.&#x20;

### Region Priority

Prioritizes low latency matches by matchmaking groups in their lowest latency regions first. Region priority sorts the latency to each region for a group into a list with the lowest latency first. It will start matchmaking the group in only the first region and will add the next region every time "Wait Per Region" elapses.  Groups will still prioritize the lower latency regions first even if they begin matchmaking in multiple regions.

<table><thead><tr><th width="224">Field</th><th>Description</th></tr></thead><tbody><tr><td><strong>Wait Per Region</strong></td><td>The amount of time in seconds to wait before adding an additional matchmaking region.</td></tr><tr><td><strong>Seconds Until Optional</strong></td><td>The amount of time in seconds until this rule no longer applies. Use this to loosen rule restrictions.</td></tr></tbody></table>

```typescript
```
