---
description: Now we need a camera that will follow around the player
---

# Custom Camera

Airship provides 3rd person and 1st person camera systems out of the box. Since we want a fixed angled camera, we will disable airships system and write our own code.

### Disable Camera System

* Click on your GameManager, AddComponent, ScriptBinding, "CharacterConfigSetup"
* Set "Movement Space" to World. (Input is not based on camera view)
* Uncheck "Use Airship Camera System"

CharacterConfigSetup is a convenience for setting global data in your scene. You can also control systems in Typescript if you prefer

```typescript
Airship.characterCamera.SetEnabled(false);
```



### Write Custom Camera Movement

Time to code our first script!&#x20;

* &#x20;In Visual Studio Code open up your typescript\~ folder
* &#x20;Run Terminal and type npm run watch to start the compiler
* Create a new script called "TopDownBattleCameraComponent"

Create the class

```typescript
export default class TopDownBattleCameraComponent extends AirshipBehaviour {
```

Add the needed variables

```typescript
@Header("References")
public camera!: Camera;
public cursorTransform!: RectTransform;

@Header("Variables")
public cameraSmoothTime = 0.3;
public lookOffsetMod = 1;

private character: Character | undefined;
private bin = new Bin();
private mouse = new Mouse();
private cameraVelocity = new Vector3();
```

Setup the events

```typescript
public override OnEnable(): void {
	if (Game.IsServer()) return; //This is a client only script

	//Stops airship from locking the cursor in game
	const mouseUnlockId = this.mouse.AddUnlocker();
	this.bin.Add(() => {
		this.mouse.RemoveUnlocker(mouseUnlockId);
	});
	//Hide the cursor so we can draw our own
	this.mouse.ToggleMouseVisibility(false);

	//Grab the local character whenever it has spawned
	this.bin.Add(
		Game.localPlayer.ObserveCharacter((entity) => {
			this.character = entity;
		}),
	);
}

public override OnDisable(): void {
	this.bin.Clean(); //Clean up event listeners
}
```

Point the character towards the cursor every frame

```typescript
public override Update(dt: number): void {
	if (this.character?.IsAlive()) {
		//Point the character towards the mouse
		const mousePos = this.mouse.GetLocation();
		let characterScreenSpacePos = this.camera.WorldToScreenPoint(this.character.model.transform.position);
		let relDir = mousePos.sub(characterScreenSpacePos).normalized;
		this.character.movement.SetLookVector(new Vector3(relDir.x, 0, relDir.y));

		//Move our custom cursor graphic
		this.cursorTransform.position = mousePos;
	}
}
```

Move the camera towards the character at the end of the frame so the movement code has already run

```typescript
public override LateUpdate(dt: number): void {
	if (this.character) {
		//Smoothly follow the character
		const [targetPos, newVelocity] = this.transform.position.SmoothDamp(
			//Character pos + the direction they are looking so you can see more of where you are aiming
			this.character.model.transform.position.add(
				this.character.movement.GetLookVector().mul(this.lookOffsetMod),
			),
			this.cameraVelocity,
			this.cameraSmoothTime,
			Time.deltaTime,
		);
		//Apply the new position
		this.transform.position = targetPos;
		this.cameraVelocity = newVelocity;
	}
}
```

add the final } and make sure all the imports were auto added. If there are any red squigglys click them then click the yellow lightbulb to auto add the imports.



### Create The Camera

* Right click in the scene and make an empty game object. Name it "CameraRig"
* Add component Script Binding, Add "TopDownBattlCameraComponent"
* Right click your CameraRIg and "Create -> Camera"
* Set the cameras transform to position(0, 6, -2.5)  rotation(60, 0, 0)
* Click your CameraRig and drag the camera in the camera



### Add the custom cursor

* Right click in the scene, "Create -> UI -> Image" to make a canvas with an image
* Delete the EventSystem if it auto made one
* Click the image, select the Images SourceImage and search for "Circleborder"
* Set the transform to width: 50 height: 50
* Click your CameraRig and drag the cursor into "CursorTransform"



Hit Play to test it out!

<figure><img src="../../.gitbook/assets/image (57).png" alt=""><figcaption></figcaption></figure>
