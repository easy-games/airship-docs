---
hidden: true
---

# AirshipNetworkBehaviour

{% hint style="danger" %}
AirshipNetworkBehaviour is a work-in-progress system. It's not recommended to use this yet. There will likely be breaking changes in the future.

Instead, use NetworkSignals.
{% endhint %}

If your Airship Component requires networking capabilities, we have `AirshipNetworkBehaviour` . This will enable networking remote procedural calls (RPCs), as well as [Networking Lifecycle Events](lifecycle-events.md) to be usable on the component.

{% code fullWidth="false" %}
```typescript
import { AirshipNetworkBehaviour, TargetRpc } from "@Easy/Core/Shared/Network";

export default class ServerWelcomeComponent extends AirshipNetworkBehaviour {
    // This is a client-only "Start" event
    public OnClientStart() {
       print("Hello, Client!");   
    }
    
    // This is a server-only "Start" event
    public OnServerStart() {
       print("Hello, Server!");
       
       Airship.Players.ObservePlayers((player) => {
          // Personalized server introduction :-)
          this.SendServerIntroduction(player, `Hello, World! - to you - ${player.username}!`);
       });
    }
    
    // TargetRpc will only send to the specified player
    // this method will also only invoke on the client it's sent to
    @TargetRpc()
    public SendServerIntroduction(player: Player, message: string) {
       Game.BroadcastMessage(`[SERVER] ${message}`);
    }
}
```
{% endcode %}
