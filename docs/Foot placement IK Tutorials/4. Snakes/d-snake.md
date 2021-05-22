---
layout: default
title: Snakes/Worms foot placement Setup
parent: Tutorials
nav_order: 4
---



## Advanced youtube tutorial


---


<div class="video-wrapper">
  <iframe width="480" height="320" src="https://www.youtube.com/embed/5F1Y12tGZhU" frameborder="0" allowfullscreen></iframe>
</div>




## Snakes/Worms foot placement Setup

---

Snakes are unique as they don't require the foot solver. Only uses the spine solver.

1) Type the pelvis and spine-start bone inside the "dragon input data". Keep the feet array empty.

1) In spine solver, increase the line trace height (above and below) value comfortably high.

2) Enable "forced activation" (optional) or tweak the values of parameters such as "Maximum feet-terrain fail distance" and "Minimum terrain-capsule activation distance".
Forced activation will provide constant stable result, but snake will be stuck completely to the ground, unable to jump.

3) Enable "is snake ?" boolean. Without this, SnakeIK will not work.


---