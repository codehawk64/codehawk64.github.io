---
layout: default
title: Common problems & solutions related to foot placement IK
parent: Tutorials
nav_order: 1
---

# Commonly encountered problems and their solutions


---


#### IK not working ?

Check if the red lines and other widgets are rendering if you click on any of the solvers. If nothing is rendered, then the IK failed to activate. The IK won't activate
if any of the bones are typed wrong. Also ensure pelvis and spine-start are typed correctly, as bad order will also cause the IK to fail.

#### IK feels like it is "turning off" on extreme slopes ?

Increase the "trace height upwards" and "trace height downwards" in the spine solver. If that doesn't help, also increase the "Maximum feet-terrain fail distance" as well as the "Minimum terrain capsule activation distance".

#### Feets floating in the air ?

Decrease the "Trace Height Upwards" in the feet solver.

#### IK reacting to too many objects in a level, including objects you don't want to react to ?

Use a custom trace channel to selectively ignore objects in the level. Create a new trace channel called "ik_channel" in the project settings under collision. Set it "ignore" by
default instead of "block". Replace the visibility channel used by the spine solvers and foot solvers. Set your terrain meshe's "ik_channel" response to block. Set objects you want the IK to ignore to "ignore".

#### Body bones rotating too much or too less ?

Tweak the "forward rotation intensity" and "sideward rotation intensity" for both the pelvis and chest in the spine solver. It is a multiplier value.

#### Feets not rotating properly when on slopes and/or when doing actions such as crouching ?

Ensure to connect a cached copy of the original pose (the pose data before it goes through the spine solver) into the foot solver's "(optional) Ref pose for feet rotation on slopes"

#### Feets are shaking or reacting too quickly towards the terrain.

Decrease or tweak the "shift speed" as well as the interpolation parameters such as "location lerp speed" and "rotation lerp speed"

#### Leg knees are bending in undesirable directions ?

- The direction of the knee bending is calculated based on the existing bends of the legs of the animation. This ensure the knee bending is perfectly natural and in-tune with the animation. If by any chance the knees are bending in an awkward direction, the animation of the legs might need to be tweaked either in the animation software, or just directly
in unreal using the personna editor. 

- Alternatively, you can also tweak the position of the blue pole widgets in the animation blueprint viewport. The knee bending will have an extra bias in the same direction of the blue pole widgets. You can directly type the data inside the feet array's "knee direction offset" parameter instead of grabbing the balls.

#### IK struggling in closed spaces like small rooms in an apartment or caves ?

Use the anti-channel functionality. Enable it in both the spine solver and foot solver. Create a new channel and call it "anti_channel" or anything comfortable with. Make sure the anti-channel's channel response is ignore by default in project settings. Objects with this anti-channel trace channel's response to "block" will repel the traces used for solving calculation. You can use meshes with the anti-channel to cover ceilings and under stairs for a customized workflow experience.


---