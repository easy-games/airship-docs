# Simple Usage

Switching between Locked and Orbit camera modes is the most common.

Switching between Locked and Orbit camera modes has been made quite easy. Simply call the `Airship.characters.localCharacterManager.SetCharacterCameraMode` method and pass in the desired camera mode type.

To set the camera to the Locked mode, use the `LOCKED` camera mode type:

```typescript
const localCharacterManager = Dependency<LocalEntityController>();

Airship.characters.localCharacterManager.SetCharacterCameraMode(CharacterCameraMode.LOCKED);
```

For more complex and custom camera setups, see the Default Camera Modes and Camera Structure pages.
