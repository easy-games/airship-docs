# Character Movement Events

```typoscript
public enum CharacterState {
    Idle = 0,
    Running = 1,
    Airborne = 2,
    Sprinting = 3,
    Crouching = 4
}

/// <summary>
/// Called whenever the movement system enters a new CharacterState.
/// </summary>
public event StateChanged stateChanged;

public enum NetworkedStateSystemMode
{
    /** The system will be used as a way to generate commands to send to an authoritative server. */
    Input,

    /** The system is the authority. It will process commands either from itself, or a remote client. */
    Authority,

    /**
     * The system is an observer. It will only be provided snapshots and will need to interpolate between
     * them to display what has already happened.
     */
    Observer,
}

/// <summary>
/// Called when the type of NetworkedStateSystemMode is set.
/// </summary>
public event Action<object> OnSetMode;

/// <summary>
/// Called when a new command is being created. This can be used to set custom data for new
/// command by calling the SetCustomInputData function during this event.
/// </summary>
public event Action<object> OnCreateCommand;

/// <summary>
/// Called on the start of processing for a tick. The state passed in is the last state of the
/// movement system.
/// Params: CharacterMovementInput input, CharacterMovementState state, boolean isReplay
/// </summary>
public event Action<object, object, object> OnProcessCommand;

/// <summary>
/// Called at the end of processing for a tick. This is after the command has been processed by
/// the move function. Use this event if you want to modify the result of the tick. Remember:
/// the resulting state from the provided input must be deterministic. Failure to have deterministic
/// state will cause unwanted resimulations.
/// Params: CharacterMovementInput input, CharacterMovementState finalState, boolean isReplay
/// </summary>
public event Action<object, object, object> OnProcessedCommand;

/// <summary>
/// Called when the movement system needs to reset to a specific snapshot
/// state. The passed object is the state that we need to reset to.
/// </summary>
public event Action<object> OnSetSnapshot;

/// <summary>
/// Called when we need to capture a given snapshot.
/// </summary>
public event Action<object, object> OnCaptureSnapshot;

/// <summary>
/// Fired every frame. Provides lastState, nextState, and delta between the two.
/// Internally this is used to position the character in the correct location for rendering
/// based upon the received network snapshots.
/// </summary>
public event Action<object, object, object> OnInterpolateState;

/// <summary>
/// Fired on fixed update, but only when a new state has been reached. We use this internally
/// to set things like animation state where interpolation between two states is not possible.
/// Provides the new state that has been reached.
/// </summary>
public event Action<object> OnInterpolateReachedState;

public event Action<object, object> OnCompareSnapshots;

public event Action<object> OnMoveDirectionChanged;

/// <summary>
/// Called when the look vector is externally set
/// Params: Vector3 currentLookVector
/// </summary>
public event Action<object> OnNewLookVector;

/// <summary>
/// Called when movement processes a new jump
/// Params: Vector3 velocity
/// </summary>
public event Action<object> OnJumped;

/// <summary>
/// Params: Vector3 velocity, RaycastHit hitInfo
/// </summary>
public event Action<object, object> OnImpactWithGround;
```
