# Camera Structure

The camera functionality has been created in such a way to be agnostic to the game it is in. The top-level class for the camera is the `CameraSystem`. Only one instance of this class should be created, and a Unity `Camera` component must be passed to its constructor.

A good practice is to create a `CameraController` that constructs the `CameraSystem` and exposes it to the game.

The whole camera system is written in TypeScript. There is no interface into this system from the C# side of the project.

## CameraMode

The `CameraSystem` works by attaching `CameraModes` to it. A `CameraMode` is a simple interface that contains basic methods like `OnLateUpdate`. These methods are responsible for calculating the position and rotation of the camera in world-space. The `OnLateUpdate` function must return a `CameraTransform`, which is a simple object that contains a position Vector3 and rotation Quaternion.

Here is an empty `CameraMode`, not yet implemented:

```typescript
class MyCameraMode implements CameraMode {
    // OnStart is called by the camera system when the mode begins.
    OnStart(camera: Camera): void {}
    
    // OnStop is called when the camera system stops this mode.
    OnStop(): void {}
    
    // OnUpdate is called during Unity's Update stage.
    // This method is useful for handling user input, and sets itself
    // at LOWEST priority on the connection, to attempt to run after
    // any other Update code has run in the game.
    OnUpdate(deltaTime: number): void {}
    
    // OnLateUpdate is called during Unity's LateUpdate stage.
    // This method must return a CameraTransform, representing the
    // camera's position and rotation. This method sets itself at
    // the HIGHEST priority on the connection, attempting to run
    // first in the LateUpdate stage before anything else.
    OnLateUpdate(deltaTime: number): CameraTransform {}
    
    // This method is called right after the Unity camera's transform has
    // been set with the data from OnLateUpdate. This might be useful if
    // other custom transforms need to be added onto the camera outside of
    // just returning a position and rotation in OnLateUpdate.
    OnPostUpdate(camera: Camera): void {}
}
```

Here is an example of a custom `CameraMode` class that spins the camera:

```typescript
class MyCameraMode implements CameraMode {
    private spinAngle = 0;
    
    constructor(private readonly spinSpeed = 3) {}
    
    OnLateUpdate(deltaTime: number) {
        // Calculate spin angle:
        this.spinAngle = (this.spinAngle + deltaTime * this.spinSpeed) % 360;
        
        // Create the Vector3 and Quaternion representing the camera in 3D space:
        const position = new Vector3(0, 0, 0);
        const rotation = Quaternion.euler(0, this.spinAngle, 0);
        
        // Create the CameraTransform, which the CameraSystem will use to set the
        // transform of the Unity camera:
        return new CameraTransform(position, rotation);
    }
    
    OnStart(camera: Camera) {}
    OnStop() {}
    OnUpdate() {}
    OnPostUpdate(camera: Camera) {}
}
```

### Running a CameraMode

In order to run a camera mode, instantiate an instance of the camera mode and set it on the `CameraSystem`:

```typescript
cameraSystem.SetMode(new MyCameraMode());
```

If the CameraSystem is exposed through a CameraController, then the full code might look more like this:

```typescript
cameraController.cameraSystem.SetMode(new MyCameraMode());

// If proxy methods are written on the controller, then perhaps:
cameraController.SetMode(new MyCameraMode());
```

### Stopping a CameraMode

There are two ways to stop a `CameraMode`.

1. Set a new `CameraMode` (this will stop the current one)
2. Clear the `CameraMode` (via `cameraSystem.ClearMode()`)

### Default Mode

This logic above for clearing the `CameraMode` has a problem. Let's say the player comes up to a shop, and the camera needs to switch to a static `CameraMode` that shows the player interacting with the shop. To do this, we simply set the new camera mode. However, what happens when the shop interaction ends? We stopped the old camera mode by setting the new one, so we can't get the old one back.

In order to solve this, we can set up a default camera mode by binding a callback function to run when the camera mode gets cleared. Any time the `ClearMode()` method gets called (_or_ if no mode has yet to be set in the game), our callback will be called, which must return a camera mode.

For example, if we wanted our spinning camera to be the default camera mode for the game, we could write the following code:

```typescript
cameraSystem.SetOnClearCallback(() => {
    return new MyCameraMode();
});
```

Now, anytime that `cameraSystem.ClearMode()` is called, our callback will run and immediately set the new mode to our custom camera mode. In an actual game, this would probably default to a camera mode that attaches to the character.

## Field Of View

The camera's field-of-view (aka FOV) represents the vertical view angle in degrees. This field can be set using `cameraSystem.SetFOV(fieldOfView)`. The CameraSystem uses a spring effect to smoothly interpolate between field-of-views. So by default, a smooth (but quick) animation between the current FOV and the new FOV will run when `SetFOV` is called. If no amination is desired, a second parameter flag can be set to `true` to represent an immediate FOV change.

```typescript
// Zoom in when right-clicking:
mouse.RightDown.Connect(() => {
    cameraSysem.SetFOV(30);
});
mouse.RightUp.Connect(() => {
    cameraSystem.SetFOV(60);
});

// Same thing, but immediate (no animation/spring effect):
mouse.RightDown.Connect(() => {
    cameraSysem.SetFOV(30, true);
});
mouse.RightUp.Connect(() => {
    cameraSystem.SetFOV(60, true);
});
```

## Input Control Responsibility

The `CameraSystem` is not responsible for handling user input to control the camera. It is up to the implementation of each `CameraMode` to handle user input. These controls should take into consideration the following items:

## Performance Responsibility

It is the responsibility of each implemented `CameraMode` to perform well. Consider the fact that methods like `OnUpdate` and `OnLateUpdate` will be running every frame, and so heavy operations could have an impact on performance. Use the profiler to test code performance.
