# User Input

Listening to user input is done through various input classes. Below are a few high-level examples of using these input classes.

For more complete documentation, please look through the other input documentation pages in this section.

### [Actions](actions.md)

```typescript
// Define an action
Airship.Input.CreateAction("Jump", Binding.Key(Key.Space));

// Listen to using the action
Airship.Input.OnDown("Jump").Connect(() => {
    print("Jump pressed")
});
```

### [Keyboard](keyboard.md)

```typescript
// Listening for key down:
Keyboard.OnKeyDown(Key.E, (event) => {
    print("Key E down");
});

// Checking if a key is currently down:
if (Keyboard.IsKeyDown(Key.E)) print("Key E down");
```

### [Mouse](mouse.md)

```typescript
// Listen for left button down and print out current screen position:
Mouse.onLeftDown.Connect(() => {
const screenPosition = Mouse.position;
    print("Left mouse button down", screenPosition);
});

// Left button up:
Mouse.onLeftUp.Connect(() => {
    print("Left mouse button up");
});

// Mouse moved:
Mouse.onMoved.Connect((screenPosition) => {
    print("Mouse moved", screenPosition);
});
```

