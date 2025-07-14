# Mouse

### Events

There are individual events for the up and down events for left, right, and middle mouse buttons: `onLeftDown`, `onLeftUp`, `onRightDown`, `onRightUp`, `onMiddleDown`, `onMiddleUp`.

```typescript
Mouse.onLeftDown.Connect(() => {
    print("Left button down");
});

Mouse.onLeftUp.Connect(() => {
    print("Left button up");
});
```

### Polling

The state of each button can also be checked with the `IsLeftButtonDown` (et. al.) methods.

```typescript
if (Mouse.IsLeftButtonDown()) {
    print("Left button down");
}

if (Mouse.IsRightButtonDown()) {
    print("Right button down");
}

if (Mouse.IsMiddleButtonDown()) {
    print("Middle button down");
}
```

## Movement

### Events

The `Moved` event fires when the mouse is moved. The `onScrolled` event fires when the scroll wheel is moved.

```typescript
Mouse.onMoved.Connect((screenPosition) => {
    print("Mouse position", screenPosition);
});

Mouse.onScrolled.Connect((delta) => {
    print("Scrolled", delta);
});
```

### Polling

Use the `position` field and `GetDelta` method to retrieve information about mouse movement.

```typescript
// Get current position of mouse:
const screenPosition = Mouse.position;

// Get movement of mouse since last frame:
const delta = Mouse.GetDelta();
```
