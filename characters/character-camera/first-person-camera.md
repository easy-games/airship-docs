---
description: >-
  To swap the character First Person, we first must set the camera mode to
  `Locked` and then set firstPerson to true.
---

# First Person Camera

```typescript
Start() {
    Airship.characters.localCharacterManager.SetCharacterCameraMode(CharacterCameraMode.Locked);
    Airship.characters.localCharacterManager.SetFirstPerson(true);
}
```
