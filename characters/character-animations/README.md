# Character Animations

## Core Animations

Airship Core has existing animations for jogging, sprinting, jumping etc. They will automatically be used on your characters but you can also customize and play your own animations.&#x20;

**There are two classes to help you control animations**

Character Animation Helper (A C# class)

Character Animator (A TS class)

{% hint style="info" %}
**Why are there two animation classes?** We need a C# to directly access some of Unity's animation features, as well as for more optimized calls that happen every frame. But we also need to capture and use data in Typescript.
{% endhint %}

***

## Animation Overrides

To play an animation on top of the core system you can use the override functions

You can play custom animations using `character.animationHelper.PlayAnimation`

```typescript
public animClip?: AnimationClip;
...
if(this.animClip){
    //Play anim clip on Override Layer 1 with a transition time of .1 seconds
    this.character.animationHelper.PlayAnimation(this.animClip, CharacterAnimationLayer.OVERRIDE_1, 0.1);
}
```

You can also replace the core animations by using an AnimationOverride asset. This allows you to drag and drop AnimationClips for specific actions without any code.

1.  Copy and paste the default AnimationOverride object into your project folder

    _"Assets/AirshipPackages/@Easy/Core/Prefabs/Character/Animations/AirshipCharacterOverrider.overrideController"_
2. In your Character prefab variant, set the animators controller to be your override asset
3.  Replace any default animation clips with your custom movement animation clips on your override controller

    <figure><img src="../../.gitbook/assets/image (79).png" alt=""><figcaption></figcaption></figure>

## Character Animation Events

Characters by default use the AnimationEventListener component to listen to animation events. You can read more about the system on the [Animation Events Page](../../unity-for-airship/animation-events.md).

To easily listen to character animation events in Typescript, connect to the OnAnimationEvent Signal on Character.animation:

```typescript
this.character.animation.OnAnimationEvent.Connect((key)=>{
    if(key === "MyAnimationEvent"){
        //Do Stuff
    }
});
```

***

## Creating New Character Animations

Animations built for the Character must match the Characters Ri&#x67;**.** The easiest way to animate for the character in Unity is to drag the CharacterAnimationDummy into your scene. This gives you bone gizmos and access to the animator at the root. Then you can use the Animation window to edit keys.

{% hint style="info" %}
You can also [Create Animations From Blender](character-blender-animations.md) by downloading our character rig animation file. You will need to setup actions for each animation and export them to an FBX file which can be brought into your Unity project.
{% endhint %}

1. Create a new AnimationClip in your project and name it
2.  Bring the animation dummy prefab in to your scene

    _"Assets/AirshipPackages/@Easy/Core/Prefabs/Character/CharacterAnimationDummy.prefab"_
3.  On the root object add your animation clip reference to the Animation component

    <figure><img src="../../.gitbook/assets/image (25).png" alt="" width="291"><figcaption></figcaption></figure>
4.  Open the Animation window and you can now select and edit your animation clip. Use the record button to auto generate keys as you move the characters rig.

    <figure><img src="../../.gitbook/assets/image (27).png" alt="" width="375"><figcaption></figcaption></figure>

{% hint style="info" %}
The Airship Character prefab is used for third person views.&#x20;

The Character View model prefab is for first person.
{% endhint %}
