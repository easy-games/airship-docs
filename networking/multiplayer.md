# Multiplayer

All games on Airship are multiplayer by default.

## Game Servers

When published, your game automatically runs with a dedicated server. This means your entire Unity project will run on the game server just as it runs on clients. Your game server will manage connecting clients and set them up as [players](https://ref.airship.gg/classes/Player.html).

<figure><img src="../.gitbook/assets/Multiplayer (2) (1).png" alt="" width="371"><figcaption></figcaption></figure>

A game server should be responsible for storing game state (such as how many coins each player has) and communicating that state to all connected players.

{% hint style="info" %}
For server ↔ client data communication see [`NetworkSignal`](network-signals.md)
{% endhint %}
