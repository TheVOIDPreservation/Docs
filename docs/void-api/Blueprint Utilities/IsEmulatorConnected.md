## `IsEmulatorConnected`

!!! warning
    This information was taken from one game, but the same logic should apply to all games. This function has been observed in all games seen so far.

This function is a utility helper designed to check for the presence of an emulator. At the moment, we don't actually know what the emulator is.

---

### Overview

| Requirement | Details |
| --- | --- |
| **Return Type** | `bool` |
| **Parameters** | `UObject* WorldContextObject` |

### Function Logic Flow

The function operates through a simple validation and retrieval sequence:

1. It attempts to locate the global instance of the `AVoidSDKManager`.
2. It checks if the `AVoidSDKManager` instance is valid (not null).
3. If valid, it queries the manager for a specific boolean setting identified by the key `"emulator.present"`.
4. It returns the value of that setting. If the manager cannot be found, it defaults to `false`.

---

### Breakdown

#### Parameters

* **`WorldContextObject`**: A pointer to an object that belongs to the current World.

#### Behavior and Edge Cases

* **Success Case:** If the SDK is active and the game is running on an emulator (like Bluestacks, Nox, or a mobile dev emulator), the function returns `true`.
* **Failure Case:** If the `AVoidSDKManager` is missing from the scene or fails to initialize, the function returns `false`.

