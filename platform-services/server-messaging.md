# Server Messaging

Game servers can communicate with each other using the built-in Server Messaging service. This provides publish/subscribe functionality for sending messages between different game servers in real-time.

## Overview

```typescript
// Server Messaging can only be used on game servers. Calls made on the client will fail.
if (!Game.IsServer()) return;

// Subscribe to a topic to receive messages
const subscription = Platform.Server.Messaging.Subscribe("player-events", (data) => {
    print("Received message:", data);
});

// Publish a message to all subscribers of a topic
Platform.Server.Messaging.Publish("player-events", {
    event: "player-joined",
    userId: "12345",
    serverName: "Battle Arena 1"
}).then((result) => {
    if (result.success) {
        print("Message published successfully");
    }
});

// Unsubscribe when no longer needed
subscription.unsubscribe();

// Alternatively, if you are using a Bin to manage resources,
// the subscription can be added directly to it.
// this.bin.Add(subscription);
```

## Use Cases

Server Messaging is useful for coordinating game state and events across multiple servers:

* **Cross-Server Events** - Notify all servers when a global event occurs (e.g., world boss spawned)
* **Player Tracking** - Share player status updates across servers
* **Global Announcements** - Send announcements that should appear on all servers

## API Reference

### Subscribe

Subscribes to a topic, allowing you to receive messages published to that topic.

```typescript
Platform.Server.Messaging.Subscribe<T>(topic: string, callback: (data: T) => void): { unsubscribe: () => void }
```

**Parameters:**

* `topic` - The topic name to subscribe to (alphanumeric characters, underscores, and hyphens only)
* `callback` - Function called when a message is received on the subscribed topic

**Returns:**

* An object with an `unsubscribe` function to stop receiving messages. This object can also be passed to a `Bin` for automatic cleanup.

### Publish

Publishes data to a topic, allowing other subscribers to receive the message.

```typescript
Platform.Server.Messaging.Publish(topic: string, data: unknown): Promise<{ success: boolean }>
```

**Parameters:**

* `topic` - The topic name to publish to (alphanumeric characters, underscores, and hyphens only)
* `data` - The data to be sent (will be JSON serialized)

**Returns:**

* A Promise that resolves to an object with a `success` boolean, set to true if publishing was successful, false if not. You can retry failed messages later or drop them

{% hint style="info" %}
Server Messaging is designed for real-time communication between servers. Sometimes messages may not be delivered, for example if there are network issues . Always check the `success` flag when publishing messages and handle failures appropriately.
{% endhint %}

## Topic Names

Topic names must follow these rules:

* Only alphanumeric characters, underscores (`_`), and hyphens (`-`) are allowed
* Topic names are case-sensitive
* Examples: `player-events`, `global_announcements`, `server123_status`

## Common Patterns

### Global Event Broadcasting

```typescript
// Broadcast a global event to all servers
interface WorldBossSpawnedEvent {
    type: "world-boss-spawned";
    location: string;
    timestamp: number;
}

interface ServerMaintenanceEvent {
    type: "server-maintenance";
    broadcastMessage: string;
}

type GlobalEvent = WorldBossSpawnedEvent | ServerMaintenanceEvent;

export class GlobalEventManager extends AirshipBehaviour {
    private bin = new Bin();

    override Start(): void {
        if (!Game.IsServer()) return;

        // Subscribe to global events
        this.bin.Add(Platform.Server.Messaging.Subscribe("global-events", (event: GlobalEvent) => {
            this.HandleGlobalEvent(event);
        }));
    }

    override OnDestroy(): void {
        this.bin.Clean();
    }

    private HandleGlobalEvent(event: GlobalEvent): void {
        switch (event.type) {
            case "world-boss-spawned":
                this.ShowWorldBossNotification(event.location);
                break;
            case "server-maintenance":
                this.ShowMaintenanceWarning(event.broadcastMessage);
                break;
        }
    }

    public BroadcastWorldBoss(location: string): void {
        Platform.Server.Messaging.Publish("global-events", {
            type: "world-boss-spawned",
            location: location,
            timestamp: os.time()
        });
    }
}
```

### Cross-Server Player Tracking

```typescript
// Track player status across servers
interface PlayerStatusUpdate {
    userId: string;
    action: "joined" | "left";
    serverId: string;
    timestamp: number;
}

export class PlayerTracker extends AirshipBehaviour {
    private playerSubscription: { unsubscribe: () => void } | undefined;
    private playerJoinedConnection: { disconnect: () => void } | undefined;
    
    override Start(): void {
        if (!Game.IsServer()) return;
        
        // Subscribe to player status updates
        this.playerSubscription = Platform.Server.Messaging.Subscribe<PlayerStatusUpdate>("player-status", (update) => {
            this.UpdatePlayerStatus(update);
        });
        
        // Notify when players join this server
        this.playerJoinedConnection = Airship.Players.onPlayerJoined.Connect((player) => {
            Platform.Server.Messaging.Publish("player-status", {
                userId: player.userId,
                action: "joined",
                serverId: Game.serverId,
                timestamp: os.time()
            } as PlayerStatusUpdate);
        });
    }
    
    private UpdatePlayerStatus(update: PlayerStatusUpdate): void {
        // Update friend lists, player counts, etc.
        print(`Player ${update.userId} ${update.action} server ${update.serverId}`);
    }
    
    override OnDestroy(): void {
        // Clean up subscription and connection
        this.playerSubscription?.unsubscribe();
        this.playerJoinedConnection?.disconnect();
    }
}
```

### Periodic Status Updates

```typescript
// Send periodic server status updates
interface ServerStatusUpdate {
    serverId: string;
    playerCount: number;
    uptime: number;
}

export class ServerStatusReporter extends AirshipBehaviour {
    override Start(): void {
        if (!Game.IsServer()) return;

        // Send status update every 30 seconds
        SetInterval(30, () => {
            Platform.Server.Messaging.Publish("server-status", {
                serverId: Game.serverId,
                playerCount: Airship.Players.GetPlayers().size(),
                uptime: Time.time,
            } as ServerStatusUpdate);
        });
    }
}
```

## Best Practices

* **Unsubscribe when done** - Always use a `Bin` or call `unsubscribe()` when you no longer need to receive messages to prevent memory leaks.
* **Use descriptive topic names** - Choose clear, consistent naming conventions for your topics
* **Handle errors gracefully** - Check the `success` flag when publishing and handle failures appropriately
* **Keep messages small** - Avoid sending large data objects; consider using references to shared data stored in the [Data Store](data-store/) or [Cache Store](cache-store.md)
* **Avoid message loops** - Be careful not to create infinite loops where servers keep responding to each other's messages

## Limitations

* Messages are not guaranteed to be delivered (fire-and-forget)
* No message ordering guarantees between different topics
* Topic names are limited to alphanumeric characters, underscores, and hyphens
* Messages are JSON serialized, so complex objects may lose information
* Server Messaging is only available on game servers, not on clients
