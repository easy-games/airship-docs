---
description: Now lets get a player running around our scene
---

# Spawn a Player Character

### Add Code To Our Scene

* In your scene create a new game object and name it "GameManager". This will be the main object that our scripts are attached to.
* In the inspector, click "add component" then search and add "Script Binding". This is a component that lets us connect a Typescipt class.
* Click "Select AirshipComponent" and search for "TopDownBattlePlayerSpawner"

This will be our starting point for our game and has some pretty standard code for spawning a player. We will break it down more as we use it throughout the tutorial.



### Spawn The Character

* Create a new Transform and name it "Character Spawn Point" and place it somewhere over the floor
* If you click on your GameManager again, you will see a variable in the inspector called "Spawn Point". Drag your spawn point transform into that variable to assign where the player will spawn.

Hit play and you should have a character running around your level! Anytime a Player joins, the character is spawned on the server by our PlayerSpawner script which then gets automatically replicated over to every client.&#x20;

```typescript
if (Game.IsServer()) {
	Airship.players.ObservePlayers((player) => {
		player.SpawnCharacter(this.spawnPosition.transform.position);
	});
}
```



### Create a Custom Character Graphic

Often a game will want to add functionality or graphics to the existing character template. Here we will setup our own prefab variant of the character to use.&#x20;

* In the project window search for "AirshipCharacter". Right click it and choose "Create -> Prefab Variant". Name it "TopDownBattleCharacter". Move this prefab into your "Shared/Resources folder" so it exists in your games package.
* Double click your TopDownBattleCharacter prefab to edit it. Right click the GraphicsHolder and choose "CreateEmpty" and name it "CharacterHighlight" to make our own place to draw graphics.
* Right click CharacterHighlights and choose "Create -> 3D -> Airship Torus". Position it at the feet and scale it down in the Y to get a highlight ring around the player. Modify the MaterialColor on this to pick a color you like.
* Now go back to your main scene and select the GameManager. Drag your character prefab from the project window into the "customCharacterTemplatme property



### (Optional) Add Accessories To Your Character

If you want custom graphics attached to the characters bones you can use our Accessory System. You can specify accessory slots to override while leaving the rest of the Players outfit in tact.&#x20;

* Create a new GameObject in the scene and name it "CharacterHelmet"
* Create an Airship Sphere inside the game object and set its MaterialColor to whatever you would like
* On CharacterHelmet click "Add Component" and select "Accessory Component"
* Set the AccessorySlot to Head
* Drag the CharacterHelmet game object into your Shared/Resources folder to create a prefab&#x20;
* Right click in the project and choose "Create -> Airship -> Accessories -> Accessory Outfit" and name it Character Outfit
* Drag your CharacterHelmet into the Outfits Accessories array. You can add more accessories to this outfit if you would like.
* Click on your GameManager in the scene and drag your Outfit into the "Character Outfit" property

The client Listens for Outfit changes and adds your custom outfit elements. Overriding slots that you have specified and leaving the rest of the players customized outfit. If you want to fully wipe users custom outfits you can call remove clothing before adding your outfit:

```
this.character.accessoryBuilder.RemoveClothingAccessories();
```
