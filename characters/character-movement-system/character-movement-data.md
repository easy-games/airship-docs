---
description: Details on the exposed variables on CharacterMovementData
---

# Character Movement Data

### Size

Control the Box Collider of the character

<div align="left"><figure><img src="../../.gitbook/assets/image (80).png" alt="" width="375"><figcaption></figcaption></figure></div>

**Height**  - controls the height of the bounding box

**Radius** - is the width and depth of the bounding box.



### Movement

core variables for moving the character

<div align="left"><figure><img src="../../.gitbook/assets/image (81).png" alt="" width="375"><figcaption></figcaption></figure></div>

**Use Acceleration Movement** - Toggle between Instant Motion and Acceleration Motion. Instant Motion drives the character instantly to the target speed. Acceleration Motion will move the character with a force over time.&#x20;

**Speed** - Desired speed to move while the character is jogging. Will instantly move to this in Instant Motion mode or stop the acceleration when it reaches this speed. In meters per second

**Sprint Speed** - Same as speed but while sprinting.

**Acceleration Force** - How fast to accelerate while in Acceleration Mode. Also controls acceleration when your character is moving faster than the target speed (ie. being flung into the air by a spring). In meters per second

**Sprint Acceleration Force** - same as Acceleration Force but while sprinting

**Min Acceleration Delta** - When moving faster than your target speed, your acceleration will be dampened if you try to acceleration in the direction you are moving. This value is a normalized minimum amount that you can move in a direction you are already moving.&#x20;

**Only Sprint Forward** - If checked, players will only be able to sprint if their velocity is moving forward



### Crouching

Specific modifiers for the crouching state

<div align="left"><figure><img src="../../.gitbook/assets/image (82).png" alt="" width="375"><figcaption></figcaption></figure></div>

Auto Crouch -&#x20;

Prevent Falling While Crouched -

Prevent Step Up While Crouched -

Crouch Speed Multiplier -

Crouch Height Multiplier -



### Jump

<div align="left"><figure><img src="../../.gitbook/assets/image (83).png" alt="" width="375"><figcaption></figcaption></figure></div>

Number Of Jumps -

Jump Speed -

Jump Coyote Time -



### Flying

<div align="left"><figure><img src="../../.gitbook/assets/image (84).png" alt="" width="375"><figcaption></figcaption></figure></div>

Number of Jumps -&#x20;

Jump Speed -&#x20;

Jump Coyote Time -&#x20;



### Gravity

<div align="left"><figure><img src="../../.gitbook/assets/image (85).png" alt="" width="375"><figcaption></figcaption></figure></div>

Use Gravity -&#x20;

Use Gravity While Grounded -&#x20;

Gravity Multiplier -&#x20;

Upwards Gravity Multiplier -&#x20;

### Gravity

How gravity effects this character

<div align="left"><figure><img src="../../.gitbook/assets/image (86).png" alt="" width="375"><figcaption></figcaption></figure></div>

Use Gravity -&#x20;

Use Gravity While Grounded -&#x20;

Gravity Multiplier -&#x20;

Upwards Gravity Multiplier -&#x20;



### Physics

<div align="left"><figure><img src="../../.gitbook/assets/image (87).png" alt="" width="375"><figcaption></figcaption></figure></div>

Prevent Wall Clipping -&#x20;

Ground Collision Layer Mask -&#x20;

Terminal Velocity -&#x20;

Minimum Velocity -&#x20;

Use minimum Velocity In Air -&#x20;

Drag -&#x20;

Air Drag Multiplier -&#x20;

Air Speed Multiplier -&#x20;



### Step Ups

<div align="left"><figure><img src="../../.gitbook/assets/image (88).png" alt="" width="375"><figcaption></figcaption></figure></div>

Detect Step Ups

Always Step Up

Assisted Ledge Jump

Max Step Up Height

Step Up Ramp Distance&#x20;



Slopes

<div align="left"><figure><img src="../../.gitbook/assets/image (89).png" alt="" width="375"><figcaption></figcaption></figure></div>

Detect Slopes -&#x20;

Slope Force -&#x20;

Min Slope Delta -&#x20;

Max Slope Delta -&#x20;
