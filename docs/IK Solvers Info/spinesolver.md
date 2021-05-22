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

| Parameter | Description                          |
|:----------|:-------------------------------------|
| dragon input data    | Type the input bones used by the solver - pelvis,spine-start and feets  |
| Precision      | Tolerance for final tip location delta from EffectorLocation                 |
| MaximumPitch      | Maximum spine rotation in pitch axis  |
| MaximumRoll      | Maximum spine rotation in roll axis    |
| MaxIterations      | Maximum number of iterations allowed.   |
| Alpha   | Alpha of the entire solver. 0 means no solving and 1 means maximum solving.  |
| Shift Speed      | The transistion speed between solve and unsolve state (eg:- when character jumps and falls back to ground). Lower values means slower but smoother transition.|
| Trace_Channel      | Trace channel used by the solver traces. Recommended to create a new dedicated trace channel for the ik through project settings.|
| Anti Trace Channel     | The repelling trace channel useful for handling close space areas. |
| Trace_Radius      | If trace type is box or sphere, its radius is controlled using the Trace Radius |
| LOD Threshold      | Max LOD that this node is allowed to run|
| Extra Dip Multiplier      |  If your character isn't dipping enough to touch the ground during slopes, slightly increase this value. Only handles dipping based on the pairs of feet and the difference between their respective trace hit location. Will not dip on flat surfaces.|
| Rotate and move bone around terrain ?      | Enable this to rotate the pelvis and chest is perfect perpendicular fashion. Good for general purpose, but can cause extreme rotation and translations in wild,sharp and uneven surfaces. Recommended to experiment between this enabled and disabled.|
| Ignore Lerping      | Disable both location and rotation interpolation|
| Trace Downward Height      | Line trace height below the spines/feets|
| Trace Upward Height      | Line trace height above the spines/feets |
| Alternate Cross Radius      |This is the spacing width of the 4 trace lines arranged in a cross pattern, around both pelvis and chest bones. Ensure the spacing radius is tweaked to the spacing of the feet. This is used for important subtle calculations, such as detecting slopes/flat surfaces. Used for rotation calculation if "Alternate cross based rotation" is enabled. |
|Maximum Feet-Terrain Fail Distance   |Maximum distance from feet to terrain to allow the solving to happen. Higher value makes the ik to solve even on terrains far below the character|
| Minimum Terrain-Capsule Activation Distance  |The minimum distance between feet and terrain to allow solving to happen. Increase this value if ik is turning off easilly on slopes. Too high of a value can make the ik to "stick" to the ground more, which can be undesirable. Recommended to tweak this value until it feels right |
| Display LineTracing  | Enable this to render the traces in the animgraph viewports.|
| Use Anti-Channel Functionality      | Use the anti-channel in the solving logic. Use meshes with the anti-channel set to "block" to repel the traces from touching ceilings and closed spaces. Also useful when under stairs or narrow multi-storied buildings. Cover the ceilings and under stairs with anti-channel blocked meshes. |
| Extra dip When going up slopes      | Extra dip when pelvis is on an upward slope |
| Extra dip When going down slopes      | Extra dip when pelvis is on a downward slope |
| Reverse Fabrik      | Enable this to prioritise chest over the pelvis. The normal fabrik mode prioritises the pelvis transformation location when on extreme terrains. The reverse fabrik mode ensures chest is given priority.|
| Calculation Relative To Ref Pose      | Should solver calculation be based on the default reference pose or the current animated pose ?|
| [Pelvis & Chest] Z Offset      | Optional additional Z offset for the [Pelvis & Chest] |
| Maximum Dip Height - [Pelvis & Chest]      | Maximum height the [Pelvis & Chest] can dip below the base pose. Lower values means [Pelvis & Chest] will dip less. For biped (2 feet) characters, this is only used. |
| Differentiate between hard flat and rotated slopes [Pelvis & Chest]     | Enable this to make the trace lines differentiate between flat planar terrains and organic terrains |
| Rotation alpha between end points      | This is the rotation alpha value of all the bones between the pelvis and chest. 1 value means full solved state, while 0 means 0 solved state.|
| Automatic Fabrik Selection (Development)      |An experimental feature, where the solver automatically switch between fabrik and reverse fabrik mode depending on the slope. |
| Body Location Lerp Speed      | Controls the location interpolation speed of the body. Higher values means faster interpolation. Slower values means slower but also smoother interpolation. |
| Body Rotation Lerp Speed      |  Controls the rotation interpolation speed of the body. Higher values means faster interpolation. Slower values means slower but also smoother interpolation.|
| Chest Influence Alpha      | The location alpha value for the chest. 1 means full solving of the chest transformation. 0 means no solving of the chest transformation. Chest rotation still works regardless.|
| [Pelvis & Chest] Forward Rotation Intensity      | Controls the intensity of the [Pelvis & Chest] forward rotation with respect to the slopes. 0 means no rotation applied.|
| [Pelvis & Chest] Sideward Rotation Intensity      | Controls the intensity of the [Pelvis & Chest] sideward rotation with respect to the slopes. 0 means no rotation applied.|
| [Pelvis & Chest] Post Rotation Offset      | Fixed rotation offsets to be applied on [Pelvis & Chest]|
| Use Alternate Cross-Based [Pelvis & Chest] Rotation      |Enable this to use the 4 cross-based trace lines to determine the rotation of the pelvis instead of the default normal method |
| Is spine always fully extended ?      | Enable this to allow spine to bend and modify at a fixed maximum length |
| Fully extended ratio      | The ratio length the spine stretches if full extension is enabled.|
| Non extended ratio      | The minimum ratio length the spine can stretch upto if full extension is disabled|
| Extension Switch Speed      | The speed of the spine extension/compression during slopes|
| Enable Solver      | Enable/Disable the solver|
| Force Activation      | This will force the ik to work at all times. Animals will not be able to jump if this is enabled. Only recommended for testing and debugging purposes.|
| accurate feet placement      | Enable this to use proper accurate feet placement logic. But it might provide jumpy nature for certain quadrupeds like horses when they are moving on slopes. Recommended use case is to disable this when a quadruped animal is moving, but enable it when it is idle.|
| use crosshair trace also for fail distance      | Enable this to use the 4 cross based traces to turn off the ik, if any of the trace hits are too far.|
| Is Biped Character ?      | Enable this to only solve the pelvis bone, while the remaining bones remain unchanged. Recommended to enable it for bipeds like humans and raptors. Also recommended for single root spiders.|
| Overall PostSolved Offset      |Additional offset parameters to the overall bones |
| Up Direction Vector      | The up direction vector of the character in component space. 99% cases, this should not be altered.|
| Forward Direction Vector      | The forward direction vector of the character in component space. 99% cases, this should not be altered. |
| Flip forward and right rotation      | If character is rigged and animated in the opposite direction to the standard unreal forward/right directions, then enable this. 99% cases, this should not be altered.|
| Solver Reference Pose      |Whether to use the reference pose or animated pose for calculations. |
| Strict Spine-Feet pair finding      | Automatically correct the spine and feet bone pairing with respect to the typed bone names in the input settings. If correct bone names are typed, it makes no difference in the end.|
| Is it a snake ?      |Enable snake mode. If character is either a snake or a worm, enable this. Can also be turned on for biped characters sleeping or proning on the ground. |
| Snake Joint Speed (If snake true)      | Spine interpolation speed if snake mode is enabled.|
