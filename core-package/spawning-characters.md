# Spawning Characters

{% hint style="info" %}
For more details on how to control and customize characters see [The Character](broken-reference) section
{% endhint %}

You can spawn characters by calling `player.SpawnCharacter()` on the server.

Example: A component that spawns characters for all players joining the server.

```typescript
export default class CharacterSpawner extends AirshipBehaviour {
    public spawnTransform! = Transform;

    override Start() {
        Airship.players.ObservePlayers((player) => {
            player.SpawnCharacter(this.spawnTransform.position);
        });
    }
}
```

### Accessing Characters

You can access a player's character through `player.character`. This is avaliable on both the server and client.&#x20;

***

## Respawn Characters on Death

```typescript
import { Airship } from "@Easy/Core/Shared/Airship";
import Character from "@Easy/Core/Shared/Character/Character";
import { Game } from "@Easy/Core/Shared/Game";

export default class CharacterSpawner extends AirshipBehaviour {
	public spawnTransform!: Transform;

	override Start(): void {
		if (Game.IsServer()) {
			// Fired when players join the game
			Airship.players.ObservePlayers((player) => {
				player.SpawnCharacter(this.spawnTransform.position);
			});

			// Fired when a character dies
			Airship.damage.onDeath.Connect((damageInfo) => {
				const character = damageInfo.gameObject.GetAirshipComponent<Character>();
				if (character?.player) {
					character.player.SpawnCharacter(this.spawnTransform.position);
				}
			});
		}
	}
}

```
