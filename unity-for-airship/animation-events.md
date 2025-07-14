---
description: >-
  Create and capture animation events to run functions in code when your
  animation hits a specific location.
---

# Animation Events

## Overview

In Airship animation events are passed to Typescript through the AnimationEventListener component. If you add this component to your animator it will pass along events from your animations. For custom data you can create a ScriptableObject of type AnimationEventData.&#x20;

{% hint style="info" %}
Naming is important here. All events must fire the function "TriggerEvent" or "TriggerEventObj" to be passed into Typescript. And the data passed must either be a string key or an AnimationEventData object.&#x20;
{% endhint %}

## Create Animation Events

To setup an event use Unity's animation event system either in the animation clip itself using the animation window, or on an FBX using the inspector window.&#x20;

1. Create a new animation event
2. Give it the function "TriggerEvent" if you have a simple trigger or "TriggerEventObj" if you want to pass more data
3. Set the triggers key to be whatever you would like to identify it by. Or set the key in the object you are passing in
   1. To create an AnimationEventData object, right click and create in the project window: "Create > Airship > Animation Event Data.
   2. Fill in the event data with whatever information you would like to listen to

<figure><img src="../.gitbook/assets/image (19).png" alt="" width="344"><figcaption><p>Simple Event On Animation Clip</p></figcaption></figure>

<figure><img src="../.gitbook/assets/image (21).png" alt="" width="375"><figcaption><p>Object Event On FBX</p></figcaption></figure>



## Listening To Animation Events

To listen to events in Typescript, get the component reference for the AnimationEventListener, then connect to the OnAnimationEvent Signal on Character.animator:

```typescript
//Get the component (or you can setup a reference if in an AirshipBehaviour)
const events = this.gameObject.GetComponent<AnimationEventListener>();
if(events){
	//Connect to simple events
	events.OnAnimEvent((key)=>{
		//Key is the string value you specify in editor
		if(key === "MyAnimationEvent"){
			///Do Stuff
			print("Heard my event!");
		}
	})
	
	//Connect to object event
	events.OnAnimObjEvent((data)=>{
		//key is used to identify the event
		if(data.key === "MyAnimationEventObj"){
			///Do Stuff with the extra data
			print("New Float: " + data.floatValue);
		}
	})
}
```

{% hint style="info" %}
Characters by default have an AnimationEventListener and can be listened to through a signal on Character.animation.OnAnimationEvent which is more performant than directly accessing the characters AnimationEventListener.

Read more on the [Character Animations Page](../characters/character-animations/)
{% endhint %}
