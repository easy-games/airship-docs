# Default Camera Modes

The camera system comes with a few pre-built camera modes.

## Humanoid Camera Mode

This camera mode is the main character camera mode. It attaches to the Humanoid component.

Most likely, this will be used as the default camera.

```typescript
cameraSystem.SetOnClearCallback(() => {
    return new HumanoidCameraMode(entity.GameObject, entity.Model);
});
```

## Orbit Camera Mode

The Orbit Camera Mode attaches the camera to a Unity Transform component and lets the user rotate the camera around the transform. The distance away from the transform is locked to the value set in the constructor.

This is a useful camera mode for observing other players or objects.

```typescript
const transform = otherEntity.gameObject.transform;
const distance = 3.5;

cameraSystem.SetMode(new OrbitCameraMode(distance, transform));
```

If you wish to use the OrbitCameraMode in the context of controlling the local player, then the entity's graphical transform must be passed to the constructor as well. This is necessary because the top-level character game object is not the same as the visual model, which will have different positioning.

```typescript
const mode = new OrbitCameraMode(
    distance,
    entity.gameObject.transform,
    entity.model.transform,
);

cameraSystem.SetMode(mode);
```

## Static Camera Mode

The Static Camera Mode simply keeps the camera in a static position and rotation.

```typescript
const position = new Vector3(0, 10, 0);
const rotation = Quaternion.identity;

cameraSystem.SetMode(new StaticCameraMode(position, rotation));
```

## Fly Camera Mode

The Fly Camera Mode allows the user to fly around the map using WASDQE keys for movement and right-click-drag for rotation.

Here is an example that sets the default camera mode to the Humanoid Camera Mode, but toggles the Fly Camera Mode when the LeftShift+P key is pressed:

```typescript
let flying = false;

// Set the default camera mode to HumanoidCameraMode:
cameraSystem.SetOnClearCallback(() => {
    return new HumanoidCameraMode(entity.GameObject, entity.Model);
});

// Toggle flight mode:
function toggleFlight() {
    flying = !flying;
    if (flying) {
        // Set the new mode to FlyCameraMode:
        cameraSystem.SetMode(new FlyCameraMode());
    } else {
        // Resets to HumanoidCameraMode since that's handled
        // in the SetOnClearCallback near the top:
        cameraSystem.ClearMode();
    }
}

// Handle key presses:
keyboard.KeyDown.Connect((event) => {
    if (!keyboard.IsKeyDown(Key.LeftShift)) return;
    if (event.Key == Key.P) {
        toggleFlight();
    }
});
```
