---
layout: default
title: Dragon Spine Solver
nav_order: 5
---

# Dragon Spine Solver

---

This solver modifies the body to adjust itself to the terrain. It does not modify the feet positions on its own, as that is handled by the Dragon Foot Solver.

## Table
---

### Input Data

| Parameter | Description                          |
|:----------|:-------------------------------------|
| dragon input data    | Type the input bones used by the solver - pelvis,spine-start and feets  |



### Solver

| Parameter | Description                          |
|:----------|:-------------------------------------|
| Precision      | Tolerance for final tip location delta from EffectorLocation                 |
| MaximumPitch      | Maximum spine rotation in pitch axis  |
| MaximumRoll      | Maximum spine rotation in roll axis    |
| MaxIterations      | Maximum number of iterations allowed.   |


### Basic Settings

| Parameter | Description                          |
|:----------|:-------------------------------------|
| Alpha   | Alpha of the entire solver. 0 means no solving and 1 means maximum solving.  |
| Shift Speed      | The transistion speed between solve and unsolve state (eg:- when character jumps and falls back to ground). Lower values means slower but smoother transition.|
| Trace_Channel      | Trace channel used by the solver traces. Recommended to create a new dedicated trace channel for the ik through project settings.|
| Anti Trace Channel     | The repelling trace channel useful for handling close space areas. |
| Trace Type | Select if using line,sphere or box trace for IK solving. |
| Trace_Radius      | If trace type is box or sphere, its radius is controlled using the Trace Radius |
| Global trace scale multiplier | Uniformly increases all trace related parameters (Trace down height,Trace up height,Max feet-terrain...distance, Min terrain-capsule...distance). I personally just use this rather than individually tweaking each trace parameter. |
| Trace Downward Height      | Line trace height below the spines/feets|
| Trace Upward Height      | Line trace height above the spines/feets |
| Use Anti-Channel Functionality      | Use the anti-channel in the solving logic. Use meshes with the anti-channel set to "block" to repel the traces from touching ceilings and closed spaces. Also useful when under stairs or narrow multi-storied buildings. Cover the ceilings and under stairs with anti-channel blocked meshes. |
| Calculation Relative To Ref Pose      | Should solver calculation be based on the default reference pose or the current animated pose ?|
| Maximum Feet-Terrain Fail Distance |Maximum distance from feet to terrain to allow the solving to happen. Higher value makes the ik to solve even on terrains far below the character|
| Minimum Terrain-Capsule Activation Distance  |The minimum distance between feet and terrain to allow solving to happen. Increase this value if ik is turning off easilly on slopes. Too high of a value can make the ik to "stick" to the ground more, which can be undesirable. Recommended to tweak this value until it feels right |

### Master Curve Settings

| Parameter | Description                          |
|:----------|:-------------------------------------|
| Use custom velocity instead of automatic character velocity for curves ? | Enable this to use your custom player velocity instead of automatically getting it from the parent character class movement component. This velocity value will be used to drive the curve parameters that depend on velocity. |
| Custom curve velocity | This is used as the velocity if "Use custom velocity..." parameter is enabled. |


### Advanced Settings

| Parameter | Description                          |
|:----------|:-------------------------------------|
| LOD Threshold      | Max LOD that this node is allowed to run|
| Rotate and move bone around terrain ?      | Enable this to rotate the pelvis and chest is perfect perpendicular fashion. Good for general purpose, but can cause extreme rotation and translations in wild,sharp and uneven surfaces. Recommended to experiment between this enabled and disabled.|
| Solving method for bones between pelvis and chest| There are 2 options, simple solving & legacy fabrik method. Legacy solving handles all the bones between the pelvis and chest through FABRIK. Simple solving avoids FABRIK for the in-between bones, and instead just linearly positions the bones. Simple method preserves pose structure better, so it could be more stable apart from being cheaper.  |
| Ignore Lerping      | Disable both location and rotation interpolation|
| Reverse Fabrik      | Enable this to prioritise chest over the pelvis. The normal fabrik mode prioritises the pelvis transformation location when on extreme terrains. The reverse fabrik mode ensures chest is given priority.|
| Alternate Cross Radius (4 green trace lines)     |This is the spacing width of the 4 trace lines arranged in a cross pattern, around both pelvis and chest bones. Ensure the spacing radius is tweaked to the spacing of the feet. This is used for important subtle calculations, such as detecting slopes/flat surfaces. Used for rotation calculation if "Alternate cross based rotation" is enabled. |
| Rotation alpha between end points      | This is the rotation alpha value of all the bones between the pelvis and chest. 1 value means full solved state, while 0 means 0 solved state.|
| Trace Interpolation Speed | This is the interpolation of the trace hit data. These work hand-in-hand with the body location interpolation speed, to create an additional layer of interpolation to provide really smooth results. |
| Body Location Interpolation Speed      | Controls the location interpolation speed of the body. Higher values means faster interpolation. Slower values means slower but also smoother interpolation. |
| Body Rotation Interpolation Speed      |  Controls the rotation interpolation speed of the body. Higher values means faster interpolation. Slower values means slower but also smoother interpolation.|
| Interpolation multiplier relative to velocity curve | This is a curve that multiplies the total interpolation with itself. X-axis is velocity and Y-value is the interpolation multiplier. Tweak this for appropriate speed of interpolation between idle & running state. |
| Chest Influence Alpha      | The location alpha value for the chest. 1 means full solving of the chest transformation. 0 means no solving of the chest transformation. Chest rotation still works regardless.|
| Enable Solver      | Enable/Disable the solver|
| Force Activation      | This will force the ik to work at all times. Animals will not be able to jump if this is enabled. Only recommended for testing and debugging purposes.|
| accurate feet placement      | Enable this to use proper accurate feet placement logic. But it might provide jumpy nature for certain quadrupeds like horses when they are moving on slopes. Recommended use case is to disable this when a quadruped animal is moving, but enable it when it is idle.|
| Accurate-Simple foot placement curve relative to velocity curve | This is a curve that switches between accurate foot placement and simple foot placement modes. X-axis is velocity. Y-value at 1 means accurate foot placement, while Y-value at 0 means simple foot placement . Tweak this for appropriate foot placement method depending on idle & running state. |
| use crosshair trace also for fail distance      | Enable this to use the 4 cross based traces to turn off the ik, if any of the trace hits are too far.|
| Solve only pelvis bone ?      | Enable this to only solve the pelvis bone, while the remaining bones remain unchanged. Recommended to enable it for bipeds like humans and raptors. Also recommended for single root spiders.|
| Avoid solving chest bone ? | This is avoid solving only the chest bone, while the rest of the bones will still be modified as usual. This can be enabled if you don't desire tweaking the rotation of the chest bone using the forward rotation intensity parameter. |
| Overall PostSolved Offset      |Additional offset parameters to the overall bones |



### Leg,Head & Tail Stabilization

| Parameter | Description                          |
|:----------|:-------------------------------------|
| Stabilize legs connected to pelvis during body bending ?  | This is to stabilize the rotation of the leg connnected to the pelvis and act independent from the body rotations. |
| (Upslope) Pelvic legs stabilization alpha  | This is an alpha that can lerp between 0 (default) and 1 (stabilized) modes for the pelvic legs if the entire body is going upslope. |
| (Downslope) Pelvic legs stabilization alpha  | This is an alpha that can lerp between 0 (default) and 1 (stabilized) modes for the pelvic legs if the entire body is going downslope.|
| Stabilize legs connected to chest during body bending ?  | This is to stabilize the rotation of the leg connnected to the chest and act independent from the body rotations.|
| (Upslope) Chest legs stabilization alpha  | This is an alpha that can lerp between 0 (default) and 1 (stabilized) modes for the chest legs if the entire body is going upslope. |
| (Downslope) Chest legs stabilization alpha  | This is an alpha that can lerp between 0 (default) and 1 (stabilized) modes for the chest legs if the entire body is going downslope. |
| (optional) Head bone to be stabilized  | Similar to the legs, the head rotation can be stabilized here. This only works if chest legs stabilization is enabled. |
| (optional) Tail bone to be stabilized  | Similar to the legs, the tail rotation can be stabilized here. This only works if pelvis legs stabilization is enabled.|


### [Pelvis/Chest]  Control Settings

| Parameter | Description                          |
|:----------|:-------------------------------------|
| Extra dip When going up slopes      | Extra dip when pelvis is on an upward slope |
| Extra dip When going down slopes      | Extra dip when pelvis is on a downward slope |
| Extra dip multiplier relative to feet lift difference      |  If your character isn't dipping enough to touch the ground during slopes, slightly increase this value. Only handles dipping based on the pairs of feet and the difference between their respective trace hit location. Will not dip on flat surfaces.|
| Pelvis gravity priority | -1 means priority of [Pelvis/Chest]dip is towards the lowest touching leg. +1 means priority of dip is towards the highest touching leg. This value can be tweaked to have a balanced overall dipping result. |
| [Pelvis/Chest] Z Offset      | Optional additional Z offset for the [Pelvis/Chest] |
| Maximum Dip Height - [Pelvis/Chest]      | Maximum height the [Pelvis/Chest] can dip below the base pose. Lower values means [Pelvis/Chest] will dip less. For biped (2 feet) characters, this is only used. |
| [Pelvis/Chest] dip height multiplier relative to velocity | This is a curve that multiplies the maximum dip height with itself. X-axis is velocity and Y-value is the dip multiplier. Tweak this for appropriate max dip when in idle and walking/running. |
| Down slope [Pelvis/Chest] forward rotation intensity      | Controls the intensity of the [Pelvis/Chest] forward rotation with respect to the slopes. 0 means no rotation applied.|
| Up slope [Pelvis/Chest] forward rotation intensity      | Controls the intensity of the [Pelvis/Chest] forward rotation with respect to the slopes. 0 means no rotation applied.|
| [Pelvis/Chest] Sideward Rotation Intensity on slopes      | Controls the intensity of the [Pelvis/Chest] sideward rotation with respect to the slopes. 0 means no rotation applied.|
| [Pelvis & Chest] Post Rotation Offset      | Fixed rotation offsets to be applied on [Pelvis/Chest]|
| Use Alternate Cross-Based [Pelvis/Chest] Rotation      |Enable this to use the 4 cross-based trace lines to determine the rotation of the pelvis instead of the default normal method |


### Experimental

| Parameter | Description                          |
|:----------|:-------------------------------------|
| Automatic Fabrik Selection (Development)      |An experimental feature, where the solver automatically switch between fabrik and reverse fabrik mode depending on the slope. |

### Spine advanced tweaks

| Parameter | Description                          |
|:----------|:-------------------------------------|
| Is spine always fully extended ?      | Enable this to allow spine to bend and modify at a fixed maximum length |
| Fully extended ratio      | The ratio length the spine stretches if full extension is enabled.|
| Non extended ratio      | The minimum ratio length the spine can stretch upto if full extension is disabled|
| Extension Switch Speed      | The speed of the spine extension/compression during slopes|

### Component direction settings

| Parameter | Description                          |
|:----------|:-------------------------------------|
| Up Direction Vector      | The up direction vector of the character in component space. 99% cases, this should not be altered.|
| Forward Direction Vector      | The forward direction vector of the character in component space. 99% cases, this should not be altered. |
| Flip forward and right rotation      | If character is rigged and animated in the opposite direction to the standard unreal forward/right directions, then enable this. 99% cases, this should not be altered.|

### Miscellaneous

| Parameter | Description                          |
|:----------|:-------------------------------------|
| Solver Reference Pose      |Whether to use the reference pose or animated pose for calculations. |
| Strict Spine-Feet pair finding      | Automatically correct the spine and feet bone pairing with respect to the typed bone names in the input settings. If correct bone names are typed, it makes no difference in the end.|

### Snake settings

| Parameter | Description                          |
|:----------|:-------------------------------------|
| Is it a snake ?      |Enable snake mode. If character is either a snake or a worm, enable this. Can also be turned on for biped characters sleeping or proning on the ground. |
| Enable Snake Interpolation | A boolean to enable the snake chain solving interpolation. Disabling it will give instant solving without any smoothening. |
| Snake Joint Speed (If snake true)      | Spine interpolation speed if snake mode is enabled.|
| Ignore tip bone modification | This can be enabled to ignore the tip bone of the chain from solving. Example usecase is the tip of the tails, as we might not want to manually control it and let it get swayed freely by the bone chain. |