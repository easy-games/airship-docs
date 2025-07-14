# TargetRpc

### Target RPC

This is for sending a function call to a specific player

{% code fullWidth="false" %}
```typescript
import { AirshipNetworkBehaviour, TargetRpc } from "@Easy/Core/Shared/Network";
export default class ExampleGlobalButton extends AirshipNetworkBehaviour {
    @TargetRpc()
    public SendMessageToPlayer(player: Player, message: string) {
        print("The server says", message, "!");
    }
    
    OnStartServer() {
        Airship.Players.ObservePlayers((player) => {
            // Will send the message to the specific player
            this.SendMessageToPlayer(player, "Hello, " + player.username + "!");
        });
    }
}
```
{% endcode %}
