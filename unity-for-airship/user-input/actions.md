# Actions

### Basic Actions

Actions let you define input bindings that your players can rebind from the settings menu.

```typescript
// Define an action
Airship.Input.CreateAction("Dash", Binding.Key(Key.LeftShift));

// Listen to using the action
Airship.Input.OnDown("Dash").Connect(() => {
    print("Dash!");
});
```

### Core Actions

You can also hook into core actions or disable them in your game. Listening to core actions allows you to share a player's preferred keybinds from other games. The `CoreAction` enum holds the ID of each core actions in Airship.

```typescript
// Disable core jump & sprint actions
Airship.Input.DisableCoreActions([CoreAction.Jump, CoreAction.Sprint]);

// Listen to core primary action (by default left click)
Airship.Input.OnDown(CoreAction.PrimaryAction).Connect(() => {
    print("Swing sword");
});
```

<figure><img src="../../.gitbook/assets/Screenshot 2024-09-13 at 2.02.00 PM.png" alt=""><figcaption><p>Settings menu after running the code snippets. Players can rebind any action without any work on your end.</p></figcaption></figure>

### Modifier Keys

For multi-key input you can create an action with a modifier key. Players can also rebind any actions to include a modifier.

```typescript
// Dash on Shift+G
Airship.Input.CreateAction("Dash", Binding.Key(Key.G, ModifierKey.LeftShift));

// Print out key display
const dashAction = Airship.Input.GetActions("Dash")[0]
const keyDisplay = dashAction.binding.GetDisplayName();
print("Press " + keyDisplay + " to dash!")
// prints "Press Left Shift + G to dash!"
```

### Update Action Binding

You can change a binding for a player through code. Unlike when a player changes their settings your binding changes will not be saved for the player beyond this session.

```typescript
dashAction.UpdateBinding(Binding.MouseButton(MouseButton.LeftButton));
```
