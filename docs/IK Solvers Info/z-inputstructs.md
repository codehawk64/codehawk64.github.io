---
layout: default
title: Major Input Structs
parent: Parameter Meanings
---

# Major Input Structs

---


This page explains the input structs used in the spine solver, feet solver and aim solver.



## Dragon Input Data (DragonData_MultiInput Struct)

This is the most important input data to supply for the aim solver to work. Everything else in the solver are optional according
to individual use case.

| Parameter | Description                          |
|:----------|:-------------------------------------|
| Start Spine/ Chest   | This is typically the chest bone. The start of the spine you want to end the calculation on. It is typically the first bone that connects the front legs.|
| Pelvis   | The pelvis bone is typically the first bone that connects the back legs, although not always. |


#### Feet Bones Array (DragonData_FootData Struct)


| Parameter | Description                          |
|:----------|:-------------------------------------|
| Feet Bone Name | self-explanatory |
|  Knee Bone Name | self-explanatory |
| Thigh Bone Name | self-explanatory |
| Feet rotation offset | This is the additional rotation offset for the feets. |
| Fixed pole ? | Enable this to use fixed pole locations instead of dynamically and naturally following the knee bone. |
| Knee pole offset | This is the extra vector offset of the knee poles. It controls the visual widget in the animbp viewport. |
| Feet trace Offset | This is the extra vector offset of the trace origins of the feet. |
| Frontal spacing (4-point feets) | This is only used if 4-point feet rotation is used. This is the space between the front point and back point. |
| Side spacing (4-point feets) | This is only used if 4-point feet rotation is used. This is the space between the left point and the right point. |
| Feet rotation limit | This is the maximum rotation allowed for the feet to rotate |
| Fixed foot height ? | Should feet heights be automatically calculated or statically defined ? Enable this for static heights. |
| Feet height offset/ Fixed feet height | Depending on whether using auto calculate or static feet heights, this parameter offsets the overall value. |
| Feet alpha | A alpha between solved feet and default unsolved feet. |
| Min feet extension ratio | This is the minimum percent the feets can compress inwards relative to the leg pose.  |
| Max feet extension ratio |This is the maximum percent the feets can extend outwards relative to the leg pose.|
| Feet slope offset multiplier | This is an extra offset of the feet z value depeding on the inclinations of the slopes. |
| Max feet lift height in UP axis | This is the maximum height the feet an lift in up direction. 0 means no limit. |
| Overrided trace radius (If capsule trace) | If its a value above 0, then the value is overrided as the new trace radius for this feet.  |

#### Feet Finger Array (DragonData_FingerData)
| Parameter | Description                          |
|:----------|:-------------------------------------|
| Finger bone name | The finger tip bone |
| Trace size scale | The finger IK use their own traces and uses the trace up and down height. This is the scale the trace height by acting as a multiplier. |
| Trace offset | An extra vector offset of the finger trace location. |
| Is finger pointing backwards ? | This is incase the fingers are pointing backwards, such as the thumbs of certain animals. |