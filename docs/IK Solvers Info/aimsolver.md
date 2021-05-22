---
layout: default
title: Dragon Aim Look Solver
parent: Parameter Meanings
---

# Dragon Aim Look Solver

---


This is a very powerful and versatile solver that handles everything related to full body aiming. Whether it is for quadrupeds,
gun aiming or even 3-point VR solving.


## Table
---

### Core input data

This is the most important input data to supply for the aim solver to work. Everything else in the solver are optional according
to individual use case.

| Parameter | Description                          |
|:----------|:-------------------------------------|
| Start Bone (Eg:- Head)    | The head bone.|
| End Bone    | The last bone to be influenced. (Eg:- Pelvis or chest) |
| LookAtLocation| Target location transform in world space |

### Optional Input Data

These are the optional inputs, such as the leg and arm data. The leg data is used for reverse IK of the feets when the body is aiming.
The hand input is needed for the arm aiming/reaching logic.

| Parameter | Description                          |
|:----------|:-------------------------------------|
|  Dragon Input Data (optional)   | Type the input bones used by the solver - pelvis,spine-start and feets. Any wrong bone typing mistake can cause the solver to fail. |
|   Hands Input (optional)  | The hand inputs. Used for seperate clamping and restricting of limb movements during body aiming. Uses : Weapon aiming, hand restriction while extreme body bending, wings stability etc|
|   Main Arm Index  | |





### Reaching & Separate Arm Aim

This section only handles the optional logic of multi-arm aiming and reaching.
If you desire dual gun aiming or even 3-point VR arm solving, then this section is your friend.

| Parameter | Description                          |
|:----------|:-------------------------------------|
|   Overrided arm aim target transform array  | Separate aim targets array for hands. Break this parameter after exposing to expose the array for dynamic modification.|
|   Hand aiming/reaching use the overrided target transform array ?  | If enabled, the overrided arm aim target array is used for the hand aiming. |
|   Hand rotations use the overrided target transforms ?  | If enabled, the arm rotation is mirrored by the target transform's rotation. |
|   Allow hand stretching ?  | If enabled, the arms can stretch beyond its original bone length constraints. |
|   Reach instead of aiming ? (Only for arms)  | Switching between arm aiming and reaching. Reaching is great when dynamically picking objects of holding something. Enable this for VR IK arms. |
|   Make hands positions influence body ? (If using multi-arm aiming)  | If enabled, the body rotation is influenced by the arm target locations. Only if reaching mode is enabled.|
|   Should arm twist when hand rotates ? (If reaching mode)  | You can completely ignore arm twisting and just twist the hands alone. |
|   Arm pole system method  | Select the pole system for the arms. Only used if reaching mode is used.|
|   Arm twist axis technique  | Choose the axis of your arm twisting. Only used if reaching mode is used. |
|   Hand rotation method  |  Decide if the hand rotation is additively calculated or directly replaced by the hand transforms. |
|   Override head rotation to use the look transform rotation ?  | If this is enabled, then the head rotation uses the rotation of the look target transform instead of aiming at the target. It can be used to set the VR hmd rotation into the head bone, to get the head rotation in all angles. |
|   Enable arm interpolation ?  | Enable this for getting arms to interpolate instead of snapping to location. Arm interpolation is different from the other interpolation parameter. |
|   Arm interpolation speed  | It's the speed of the arm interpolation.|



### Advanced Clamping Settings

All your core clamping parameters are held here. Whether it is for the head,body,arms or even the overall max-min clamp of everything.

| Parameter | Description                          |
|:----------|:-------------------------------------|
|   Max Body Lookat Clamp  | The maximum allowed body chain rotation. Uses the body clamp curve as a multiplier for the final result. |
|   Inner Body Lookat Treshold  | This is a treshold angle limit for the body aiming. If the angles cross this treshold, then the bones will start the aiming process.|
|  Head Max Clamp   |  Maximum separate limbs clamp. Can be used to shrink the angle or extend the angle with respect to the body clamp. Ignored if seperate head clamp bool is disabled. |
|   Limbs Max Clamp  | Maximum separate limbs clamp. Can be used to shrink the max angle or extend the max angle with respect to the body clamp. |
|  Max Vertical Angle Range (Degrees)   |  Max global vertical rotation clamp. Beyond these clamps, the aiming reverses. |
|   Max Horizontal Angle Range (Degrees)  | Max global horizontal rotation clamp. Beyond these clamps, the aiming reverses. |


### Multiplier Settings

These are multiplier parameters that helps fine-tune the body dipping logic in various scenarios.

| Parameter | Description                          |
|:----------|:-------------------------------------|
|   Downward translation when aiming upwards (Multiplier)  | The extra dip downwards if character is looking vertically upwards. |
|   Downward translation when aiming downwards  | The extra dip downwards if character is looking vertically downwards.|
|   Vertical Dip Treshold  | This is the "gap" until the body starts to dip when aiming downwards. |
|   Sideward translation when aiming sideways (Multiplier)  | The extra offset of the root bone in left/right if character's end bone is rotating towards the same direction. |
|   Downward translation when aiming sideways (Multiplier)  | The extra offset of the root bone in left/right if character's root bone is rotate towards the same direction. |
|   Vertical aim clamp ratio for body  | Tweak this if you want the clamp intensity to be different in the vertical axis. It is a multiplier ratio, and clamp is relative to existing setup. 0 = Absolutley no vertical body bending/aiming. 1 = Full Vertical body bending/aiming. Only applies to body chain. Ignores arms and head. |

### Curve Input Settings

There are the curve parameters that work in tangent with other parameters.

| Parameter | Description                          |
|:----------|:-------------------------------------|
|  Bone Clamp Curve   | Curve clamp used to tweak the body bending limits. Works as a multiplier and is part of the total solving calculation. 0th value in X-axis denotes the clamp intensity of the end bone (eg:- if max body clamp is 100, and the 0th value is 0.1, then the final clamp of pelvis/end bone is 10). All values until the 1st value in the X-axis are multipliers for all the bone chains from End to Start bones. Exact 1st X-axis value is ignored, as the head clamp is solely determined by the separate head clamp parameter.|
|  Body Rotation Multiplier Curve   | Curve multiplier to tweak the rotation multiplier in the body chain. Default set to 1 always. No need for modification in most cases.|


### Toggle Settings


| Parameter | Description                          |
|:----------|:-------------------------------------|
|   Should feets be locked using IK ?  | Lock legs to its original position using IK as the body moves and rotates. Only works with valid dragon input data.|
|  Ignore Elbow Compression   | Only rotate the shoulder towards the target, and ignore the wrist and elbow in the solving. |
|  Ignore Seperate Hand solving   | Turn off separate limbs aiming. |
|   Use Relative Rotation Algorithm ?  | Switch between two different rotation algorithm for different type of results. [enabled] = Relative rotation algorithm provides greater degree of freedom of movement and stable poses. Favours pose stability over accuracy. [disabled] = Non-Relative rotation algorthm provides a more direct and natural aiming but with limit in the range of motion. Favours accuracy over pose stability. |
|  Use Separate independent clamping for head ?   | If enabled, the heads clamp is determined by the separate max head clamp parameter. If disabled, the head clamp is determined by the value in the clamp curve graph along with the rest of the body. Also influenced by max body clamp parameter.If using the aim solver for tails, keep this disabled.|
| Head use exact accurate aiming ? | If enabled, head aims exactly at the target regardless of the rest of the body chain. If disabled, head aims while adjusting itself with respect to the rest of the body chain. Can result in a bit more stable but offseted aiming.|
|  Enable Solver   | Toggle this parameter to instantly turn on/off ik. |
|  Automatic Foot-Knee-Thigh detection   | Parameter to choose between automatic feet bone detection or manual method. If enabled, solvers only uses the feet bones, and automatically assumes the next 2 parent bones as knees and thighs. If disabled, solvers uses the feet bones, knee bones and thigh bones typed in the feet array. If disabled, all bones need to be valid. Any invalid bones will not activate the ik. Very useful to keep it disabled on DAZ rigs and certain animal characters, where the thigh-knee-foot are not in a straight linear hierarchy. |
|  Work outside gameplay (For sequencer)   | Enable this to make the solvers calcualte everytime, even during non-gameplay scenarios. Such as sequencer recording sessions.  |


### Tail Terrain Settings

This is a special section that makes the bone chain to adapt to the terrain. It can be used for long necks of a dragon, or even long tails of a character.
A single trace line is fired for the terrain solving calculation if using these features.

| Parameter | Description                          |
|:----------|:-------------------------------------|
|  Is it a terrain addaptive chain ? (like tails)   | Enable this to turn this solver into an automatic terrain adaptive chain. The lookatlocation parameter is disabled here, in favour of the debuglooklocation as the base reference of the height. The viewport look widget will be used as reference for the in-game terrain adaption. |
|  TAC Collision channel   | Trace channel used by the solver traces. Recommended to create a new dedicated trace channel for the ik through project settings. |
|  Trace Up Height   | This is the upward height of the trace from the lookat widget. |
|  Trace Down Height   | This is the downward height of the trace from the lookat widget. |


### Interpolation Settings

| Parameter | Description                          |
|:----------|:-------------------------------------|
|  Interpolation Type   | Select the type of interpolation method. |
|  Enable Interpolation   | A boolean to enable/disable overall interpolation. Arms interpolation is independent.  |
|  Interpolation Speed  | Speed of solving interpolation. |
|  Toggle Interpolation Speed  | Speed of interpolation between toggling the on/off state of the aim IK.|

### Look At Settings

All the forward and upward axis of the character can be defined here. Tweak according to the general direction the character faces in component space.

| Parameter | Description                          |
|:----------|:-------------------------------------|
|  Forward Axis   | The forward direction axis of the character. Characters using the standard unreal directions use the default value.|
|  Upward Axis   | The up direction axis of the character. Characters using the standard unreal directions use the default (0,0,1) value.|
|  Target Offset (only for limbs)   | Useful for tweaking the aiming offset of arms/limbs. Popular use is for weapons aiming and accuracy. Offset works in component space. |
|  Use Reference Forward Axis Logic ?   | If using mocap or any use case that involves altering the forward axis during gameplay, this can be enabled to dynamically alter the arm and leg poles along with the along with the change in axis. The forward axis is compared with the reference forward axis to calculate the offset of the poles. If they are the same, then nothing happens.|
|  Reference Forward Axis   | This parameter is mainly useful when using mocap animations that involves the character rotating its root bone in multiple directions. It is the default forward vector of your character in component space. The forward vector is compared with the reference forward vector to appropriately alter the knee poles and elbow poles and correcting them. If your character is setup in standard unreal forward axis, then there is no need to alter this.|


### Debugging Only

There are mainly used for debugging purposes, such as the widget locations.

| Parameter | Description                          |
|:----------|:-------------------------------------|
|Debug Look at Location | Used for internal animation blueprint viewport for debugging. Real gameworld uses "LookAtLocation".If Tail Terrain Adaptive mode is enabled, then this is turned into a constant height reference point from which the line trace is fired. |
| Debug Hand Locations| Used for internal animation blueprint viewport debugging when using separate arms aiming/reaching. This does not influence the game world arm transforms |