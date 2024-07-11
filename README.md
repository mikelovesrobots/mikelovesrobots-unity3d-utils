# mikelovesrobots-unity3d-utils

Misc Unity3d utils I've created and find useful.
Last tested against Unity 2022 LTS.

# Installation

This is too raw and miscellany to turn into a package for general use at this time. Just copy the mikelovesrobots-unity3d-utils folder
into your project into the assets folder. You're also going to need to add this tweening library to the package manager:

- git+https://github.com/jeffreylanters/unity-tweens

# State Machine

Includes StateMachine.cs and State.cs. Inherit your states from State.cs and place them on child gameObjects beneath StateMachine.

For example:

```
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class StartGameState : State
{
    public float delayBeforeTransition = 2.0f;
    public StateMachine stateMachine;
    public State nextState;

    public override void OnEnterState()
    {
        StartCoroutine(WaitForFadeInThenTransition());
    }

    IEnumerator WaitForFadeInThenTransition()
    {
        yield return new WaitForSeconds(delayBeforeTransition);
        stateMachine.SwitchState(nextState);
    }

    public override void OnExitState()
    {
        // Left empty for demonstration purposes
    }
}
```

# SceneChanger Prefab

Manages fade-in/fade-out when entering/leaving a scene.

It auto-fades in when the scene loads.

Call `SceneChanger.Instance.ChangeScene(sceneName)` to fade-out and then change scenes.
