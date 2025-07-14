# Keyboard

Keyboard API is useful for directly accessing keystrokes. If you want players to rebind your input use [Actions](actions.md).

## Listening for Key Presses

Use the `OnKeyDown` and `OnKeyUp` methods to listen for key events.

```typescript
Keyboard.OnKeyDown(Key.E, (event) => {
    print("E key down");
});

Keyboard.OnKeyUp(Key.E, (event) => {
    print("E key up");
});

// Optional signal priority:
Keyboard.OnKeyDown(Key.E, (event) => {
    print("E key down, before the other one!");
}, SignalPriority.HIGH);
```

### Disconnecting Listener

Keyboard listeners return a cleanup function. When you no longer need to listen to the key you can call the cleanup function to disconnect your callback.

```typescript
// Listen for one press of "E" -- then disconnect
const disconnectKeyDownE = Keyboard.OnKeyDown(Key.E, (event) => {
    print("E key down");
    // Disconnect this listener
    disconnectKeyDownE();
});
```

## Polling for Keys Down

To check if an individual key is down, call the `IsKeyDown` method. There are also two combination methods, `IsEitherKeyDown` and `AreBothKeysDown`.

```typescript
// Check if single key is down:
if (Keyboard.IsKeyDown(Key.E)) print("E is down");

// Check if at least one of the two keys are down:
if (Keyboard.IsEitherKeyDown(Key.W, Key.UpArrow)) print("Up");

// Check if both keys are down:
if (Keyboard.AreBothKeysDown(Key.S, Key.LeftShift)) print("Save");
```

## Sinking Key Events

It is possible to sink key input events, preventing the event from continuing on to other listeners.

To sink an event, use the `SetCancelled` event method. In cases where event sinking is occurring, it is best to also include the desired `SignalPriority`.

```typescript
Keyboard.OnKeyDown(Key.E, (event) => {
    event.SetCancelled(true);
}, SignalPriority.HIGHEST);
```
