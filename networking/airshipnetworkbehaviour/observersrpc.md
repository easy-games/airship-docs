# ObserversRpc

### Observers RPC

This is for broadcasting a call to all clients from the server.

<pre class="language-typescript" data-full-width="false"><code class="lang-typescript">import { AirshipNetworkBehaviour, ObserversRpc } from "@Easy/Core/Shared/Network";
<strong>export default class ExampleGlobalButton extends AirshipNetworkBehaviour {
</strong>    @ObserversRpc()
    private BroadcastMessage(string message) {
        print("Server has sent everyone", message, "!")
    }
}
</code></pre>
