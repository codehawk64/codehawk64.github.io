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

| Parameter | Description                          |
|:----------|:-------------------------------------|
| dragon input data    | Type the input bones used by the solver - pelvis,spine-start and feets  |
| IK Type   |  Select foot ik type - two bone ik and one bone ik. 99.9% best to use the default two bone ik. One bone ik is only useful in case the animal has no knee bones, such as the infinity blade spiders.  |
| Trace Type   | Choose Trace type - Line,Sphere and Box.  |
| Trace Radius   | If trace type is box or sphere, its radius is controlled using the Trace Radius  |
|  Location Interpolation Type  | Select the feet location interpolation method. Default uses the divisive location interpolation method, which provides optimal smoothness and speed of solving. Optionally can use the legacy method of interpolation.  |
| Rotation Interpolation Type   | Select the feet rotation interpolation method. Default uses the divisive location interpolation method, which provides optimal smoothness and speed of solving. Optionally can use the legacy method of interpolation.  |
| Automatic leg Make   | Parameter to choose between automatic feet bone detection or manual method. If enabled, solvers only uses the feet bones, and automatically assumes the next 2 parent bones as knees and thighs. If disabled, solvers uses the feet bones, knee bones and thigh bones typed in the feet array. If disabled, all bones need to be valid. Any invalid bones will not activate the ik. Very useful to keep it disabled on DAZ rigs and certain animal characters, where the thigh-knee-foot are not in a straight linear hierarchy.|
| Use (optional ref pose) as reference for foot rotation ?   | If enabled, the rotation of the feet will be relative to its current animation. If disabled, the absolute reference rotation of the feet will be used instead, ensuring always aligned feets. |
| Enable Solver   |  Toggle this parameter to turn on/off ik. Example use case : Disable it when character is jumping or flying in the air. |
|  Shift Speed  |  The transistion speed between solve and unsolve state of the leg ik (eg:- when character jumps and falls back to ground). Lower values means slower but smoother transition. |
|  Feet Position Interpolation Speed  |  Controls the feet interpolation location speed. Lower values means smoother but slower results. Is ignored if "Ignore location lerping" is enabled. |
|  Feet Rotation Interpolation Speed  |  Controls the feet interpolation rotation speed. |
|  Trace_Channel  |  Trace channel used by the solver traces. Recommended to create a new dedicated trace channel for the ik through project settings. |
|  Anti_Trace_Channel  |  Channel used for the trace repelling anti-channel process. |
|  Trace Height above feet  | Line trace height above the feet bones. Too high values will cause legs to react to ceilings and trees. Too low values will cause ik to not work on extreme slopes and steps. |
|  Trace Height below feet  | Line trace height below the feet bones. Usually best kept 0. Too high values can lead to sticky IK which might be undesirable.  |
|  Use Anti-Channel Functionality  | Use the anti-channel in the solving logic. Use meshes with the anti-channel set to "block" to repel the traces from touching ceilings and closed spaces. Also useful when under stairs or narrow multi-storied buildings. Cover the ceilings and under stairs with anti-channel blocked meshes.  |
|  Ignore Rotation Lerping  |  Enable this to completely bypass rotation interpolation and use default values! |
| Ignore Location Lerping | nable this to completely bypass location interpolation and use default values!|
| Should Solving Rotate Feet ? |Disable this to ignore feet rotaion and use default animated rotation. |
| Display Line Trace ? | Enable this to render the line traces in the animgraph viewport.|
| Enable Foot Pitch | Disable this to zero out the pitch of the feet.|
| Enable Foot Roll | Disable this to zero out the roll of the feet.|
| Character Up Direction Vector (Local space) |The up direction vector of the character in component space. 99% cases, this should not be altered. Only needed to alter on characters that do not follow the standard unreal character orientations. |
| (optional) Foot x Height offset | Extra feet height offsets that can be altered during gameplay. |
