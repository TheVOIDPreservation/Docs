## `DebugJumpToScenario`

!!! danger
    This is based on a decompilation of WIR only, and it's internal functionality DOES vary between titles; exact behavior for other games with this function has not yet been confirmed. Additionally, it's no longer seen in the newer games like Jumunji. 

Debug-jumps the active scenario to a matching Scenario. Believed to be used primarily for development and testing to force the manager to make a specific scenario active.

---

### Overview

| Requirement | Details |
| --- | --- |
| **Return Type** | `None` |
| **Parameters** | `Scenario` (Object varies depending on game) |

### Function Logic Flow

The function operates through the following sequence:

1. **Null check**: Return immediately if `Scenario` is `nullptr`.
2. **Ensure array not empty**: Verify `m_Scenarios.Num()` is greater than zero.
3. **Find matching pointer**: Iterate `m_Scenarios` and compare each element's `ScenarioPointer` to `Scenario`.
4. **Set active scenario**: If a match is found, obtain the `FScenarioInfo` pointer and call `SetActiveScenario(Info)`.

---

### Breakdown

#### Parameters

* **`Scenario`**: Pointer to the Scenario. If `nullptr`, the function exits without side effects.

#### Behavior and Edge Cases

* **Success Case:** When a matching `ScenarioPointer` is found in `m_Scenarios`, the corresponding `FScenarioInfo` is passed to `SetActiveScenario()` and the manager switches to that scenario.
* **Failure Case:** If `Scenario` is `nullptr`, or `m_Scenarios` is empty, or no matching pointer is found, the function returns without changing state.

