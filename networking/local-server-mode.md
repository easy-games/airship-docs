# Local Server Mode

We have two formats for server mode during local development: [Dedicated](local-server-mode.md#dedicated) and [Shared](local-server-mode.md#shared). You can swap your development mode by pressing the toggle left of the play button:

<figure><img src="../.gitbook/assets/Screenshot 2024-07-03 at 2.41.36 PM.png" alt="" width="563"><figcaption></figcaption></figure>

## Dedicated

Local development in dedicated mode mimics how a published game will run. In dedicated you will need one Unity editor instance for each connected client and one for the server.

We use **Multiplayer Play Mode** (MPPM) to manage multiple editor windows. Each window represents a different client (with one for the server).

How to setup a dedicated server using MPPM:

1. Open menu item `Window > Multiplayer Play Mode`
2. Tag Player 2 with Server (`Add Tags for Player > Server`)
3. Check the box left of Player 2 (this should open your server window)

<figure><img src="../.gitbook/assets/Screenshot 2024-07-03 at 1.56.01 PM (1).png" alt="" width="375"><figcaption></figcaption></figure>

## Shared

Shared mode doesn't require multiple editor windows. Instead, your single window will function as both the client and server. Both `Game.IsServer()` and `Game.IsClient()` will return `true`. This is useful because time-to-play becomes faster. The downside is that the game behaves differently in editor than when published on a dedicated server.&#x20;

{% hint style="warning" %}
Shared mode will behave differently from a published game. You should make sure to test your game in dedicated before publishing.
{% endhint %}
