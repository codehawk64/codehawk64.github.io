---
layout: default
title: Dragon Foot Solver
parent: Parameter Meanings
---


# Dragon Foot Solver

---

This solver modifies the legs of the character to adjust them to the terrain. It typically works complimentary with the spine solver.

## Table

---

### Input Data

| Parameter | Description                          |
|:----------|:-------------------------------------|
| dragon input data    | Type the input bones used by the solver - pelvis,spine-start and feets  |


### Trace Settings

| Parameter | Description                          |
|:----------|:-------------------------------------|
| IK Type   |  Select foot ik type - two bone ik and one bone ik. 99.9% best to use the default two bone ik. One bone ik is only useful in case the animal has no knee bones, such as the infinity blade spiders.  |
| Trace Type   | Choose Trace type - Line,Sphere and Box.  |
| Trace Radius   | If trace type is box or sphere, its radius is controlled using the Trace Radius  |
|  Trace_Channel  |  Trace channel used by the solver traces. Recommended to create a new dedicated trace channel for the ik through project settings. |
|  Anti_Trace_Channel  |  Channel used for the trace repelling anti-channel process. |
| Fps treshold for interpolation | If frame rate falls below this treshold, then interpolation is disabled for instant results as well as better overall performance. |
|  Trace Height above feet  | Line trace height above the feet bones. Too high values will cause legs to react to ceilings and trees. Too low values will cause ik to not work on extreme slopes and steps. |
|  Trace Height below feet  | Line trace height below the feet bones. Usually best kept 0. Too high values can lead to sticky IK which might be undesirable.  |
| Global trace scale multiplier | Uniformly increases all trace related parameters. Increase this value if your mesh is super big by default and you are too lazy to increase all parameters one by one. I personally just use this rather than individually tweaking the trace heights.|
| Trace down height multiplier relative to velocity | This is a curve parameter that multiplies with the "Trace height below feet" relative. |
|  Use Anti-Channel Functionality  | Use the anti-channel in the solving logic. Use meshes with the anti-channel set to "block" to repel the traces from touching ceilings and closed spaces. Also useful when under stairs or narrow multi-storied buildings. Cover the ceilings and under stairs with anti-channel blocked meshes.  |


### Master Curve Settings

| Parameter | Description                          |
|:----------|:-------------------------------------|
| Use custom velocity instead of automatic character velocity for curves ? | Enable this to use your custom player velocity instead of automatically getting it from the parent character class movement component. This velocity value will be used to drive the curve parameters that depend on velocity. |
| Custom curve velocity | This is used as the velocity if "Use custom velocity..." parameter is enabled. |


### Interpolation Settings

| Parameter | Description                          |
|:----------|:-------------------------------------|
|  Location Interpolation Type  | Select the feet location interpolation method. Default uses the divisive location interpolation method, which provides optimal smoothness and speed of solving. Optionally can use the legacy method of interpolation.  |
| Rotation Interpolation Type   | Select the feet rotation interpolation method. Default uses the divisive location interpolation method, which provides optimal smoothness and speed of solving. Optionally can use the legacy method of interpolation.  |
| Interpolate only on legs Z axis ? | If enabled, interpolation is strictly on the vertical axis of the feets. If disabled, interpolation is in all axis. Might create a delayed feet response in low frame rates if interpolating in all 3 axis.|
|  Shift Speed  |  The transistion speed between solve and unsolve state of the leg ik (eg:- when character jumps and falls back to ground). Lower values means slower but smoother transition. |
|  Feet Position Interpolation Speed  |  Controls the feet interpolation location speed. Lower values means smoother but slower results. Is ignored if "Ignore location lerping" is enabled. |
|  Feet Rotation Interpolation Speed  |  Controls the feet interpolation rotation speed. |
| Ignore shift logic | Shift logic is the smooth transition between solving and non-solving state. Such as if the feet traces are touching the ground. Ignoring shift logic will make transitions instant. |
|  Ignore Rotation Interpolation  |  Enable this to completely bypass rotation interpolation and use default values! |
| Ignore Location Interpolation | Enable this to completely bypass location interpolation and use default values!|
| Interpolation multiplier relative to velocity curve | This is a curve that multiplies the total interpolation with itself. X-axis is velocity and Y-value is the interpolation multiplier. Tweak this for appropriate speed of interpolation between idle & running state. |
| Enable complex but accurate foot placement method ? | Enabling this will 100% accurately place your feet position and rotation according to the terrain normal data without any gaps between the feet and terrain, but might sacrifice stability. Your leg poses might appear too "stylish" or "Jojo" if the terrain is too crazy due to over extending. Best to try it out and see if you if its good for your needs. |
| Complex to simple foot placement transition relative to velocity | Only used if complex foot placement is used. Turn off complex feet and switch to simple feet IK during locomotion for the best of both methods for maximum stability. Y-axis 1 means complex and 0 means simple. X-axis is character velocity. Default value basically switches to complex |


### Basic Settings

| Parameter | Description                          |
|:----------|:-------------------------------------|
| Automatic foot-knee-thigh detection   | Parameter to choose between automatic feet bone detection or manual method. If enabled, solvers only uses the feet bones, and automatically assumes the next 2 parent bones as knees and thighs. If disabled, solvers uses the feet bones, knee bones and thigh bones typed in the feet array. If disabled, all bones need to be valid. Any invalid bones will not activate the ik. Very useful to keep it disabled on DAZ rigs and certain animal characters, where the thigh-knee-foot are not in a straight linear hierarchy.|
| Use (optional ref pose) as reference for foot rotation ?   | If enabled, the rotation of the feet will be relative to its current animation. If disabled, the absolute reference rotation of the feet will be used instead, ensuring always aligned feets. |
| Enable Solver   |  Toggle this parameter to turn on/off ik. Example use case : Disable it when character is jumping or flying in the air. |
| Should Solving Rotate Feet ? |Disable this to ignore feet rotaion and use default animated rotation. |
| Enable Foot Pitch | Disable this to zero out the pitch of the feet.|
| Enable Foot Roll | Disable this to zero out the roll of the feet.|
| Character Up Direction Vector (Local space) |The up direction vector of the character in component space. 99% cases, this should not be altered. Only needed to alter on characters that do not follow the standard unreal character orientations. |
| Dynamic forward direction vector (Local space) |The up direction vector of the character in component space. 99% cases, this should not be altered. Only needed to alter on characters that do not follow the standard unreal character orientations. |
| Reference forward direction vector (Local space) |The up direction vector of the character in component space. 99% cases, this should not be altered. Only needed to alter on characters that do not follow the standard unreal character orientations. |
| Use advanced 4-point feet rotation ? | This is a new alternative method of rotating the feets. Instead of calculating from the normal data of the terrain, the rotation is calculated from approximating the results of the position of the 4 traces. 4-line traces around the feet. This helps rotate the feets even on sharp terrains more logically.   |
| Enable foot lift limit ? (Uses the foot extension ratios in foot array) | Enable the ability to limit the lift of the feets. This limit is controlled from the feet array. |
| Calculate toe/finger rotations ? | Enable this to unlock and use the finger solving algorithm for each defined finger in the feet array. |
| Finger IK alpha relative to velocity | This is a curve that multiplies the finger IK alpha with itself. X-axis is velocity and Y-value is the finger alpha multiplier. Default value basically disables finger IK during locomotion. |
| Minimum allowed leg IK angle | This is the clamping of the leg IK accordingly  |
| Work outside gameplay (for sequencer) | Enable this for having the IK work even outside gameplay, such as in the editor during sequencer recordings. |

### Dynamic foot offset

| Parameter | Description                          |
|:----------|:-------------------------------------|
| (optional) Foot x height offset | These are optional feet height offsets which be comfortably and dynamically modified for your purpose, instead of creating programatically creating inputs and supplying it. |

### Performance

| Parameter | Description                          |
|:----------|:-------------------------------------|
| LOD Treshold | The maximum LOD the IK solver will work with. -1 means the solver will work at all LOD levels. |