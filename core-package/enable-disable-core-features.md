---
description: >-
  To easily configure your project you can add the CharacterConfigSetup
  component to any game object in your scene.
---

# Enable / Disable Core Features

* Click on your game object
* Add Component: "Script Binding"
* Click "Add Airship Component"
* Search and select "CharacterConfigSetup"

You now can control many of the core systems. These toggles will fire as soon as your scene is loaded.&#x20;

<figure><img src="../.gitbook/assets/image (66).png" alt="" width="367"><figcaption></figcaption></figure>

If you need to control these options dynamically, they are all accessible via TS

```typescript
public OnEnable() {
	//Character
	//Set the default prefab to use whenever a character is spawned
	Airship.characters.SetDefaultCharacterPrefab(this.customCharacterPrefab);

	//Local Character Configs
	if (Game.IsClient()) {
		//Movement
		//Control how client inputs are recieved by the movement system
		Airship.characters.localCharacterManager.SetMoveDirWorldSpace(this.movementSpace === Space.World);

		//Camera
		//Toggle the core camera system
		Airship.characterCamera.SetEnabled(this.useAirshipCameraSystem);
		if (this.useAirshipCameraSystem) {
			//Allow clients to toggle their view model
			Airship.characterCamera.canToggleFirstPerson = this.allowFirstPersonToggle;
			if (this.startInFirstPerson) {
				//Change to a new camera mode
				Airship.characterCamera.SetCharacterCameraMode(CharacterCameraMode.Locked);
				//Force first person view model
				Airship.characterCamera.SetFirstPerson(this.startInFirstPerson);
			}
		}

		//UI visual toggles
		Airship.chat.SetUIEnabled(this.showChat);
		Airship.inventory.SetBackpackVisible(this.showInventoryBackpack);
		if (this.showInventoryHotbar || this.showHealthbar) {
			Airship.inventory.SetUIEnabled(true);
			Airship.inventory.SetHealtbarVisible(this.showHealthbar);
			Airship.inventory.SetHotbarVisible(this.showInventoryHotbar);
		} else {
			Airship.inventory.SetUIEnabled(false);
		}
	}

	//Stop any input for some movement options we don't use
	if (!this.enableJumping || !this.enableCrouching || !this.enableSprinting) {
		//Listen to input event
		Airship.characters.localCharacterManager.onBeforeLocalEntityInput.Connect((event) => {
			//Force the event off if we don't want that feature
			if (!this.enableJumping) {
				event.jump = false;
			}
			if (!this.enableCrouching) {
				event.crouchOrSlide = false;
			}
			if (!this.enableSprinting) {
				event.sprinting = false;
			}
		});
	}
}
```
