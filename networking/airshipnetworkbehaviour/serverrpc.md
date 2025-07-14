# ServerRpc

The server RPC allows logic to be ran on the server from a client - by default it will not require any ownership - so can be run by any player. This wont run on the client who called it unless `RunLocally` is `true`.

{% code fullWidth="false" %}
```typescript
import { AirshipNetworkBehaviour, ServerRpc } from "@Easy/Core/Shared/Network";

export default class ExampleGlobalButton extends AirshipNetworkBehaviour {
    // This will send a button press message to the server _only_
    @ServerRpc()
    public PressButton(player: Player, message: string) {
        // Player argument necessary if not requiring ownership
        print("The player", player, "pressed the button with their message", message);
    }
}
```
{% endcode %}

{% hint style="info" %}
Note: If you want to restrict to only the network owner of the component, you must specify `RequiresOwnership`as `true`

<pre class="language-typescript" data-full-width="true"><code class="lang-typescript">import { AirshipNetworkBehaviour, ServerRpc } from "@Easy/Core/Shared/Network";
<strong>export default class ExamplePlayerInventory extends AirshipNetworkBehaviour {
</strong>    @ServerRpc({ RequiresOwnership: true })
    public DropItemFromInventory(itemId: ItemType, amount: number) {
        // Note: No player argument as this is guaranteed to be the owner
    }
}
</code></pre>
{% endhint %}
