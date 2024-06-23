---
title: Frozen Depths
description: This was my final project at AIE Melbourne
date: 2021-12-01 00:00:00+0000
slug: frozen-depths
image: frozen-depths-cover.png
categories:
    - Hobby Projects
tags:
    - Unity
    - C#
    - Game Development
weight: 1       # You can add weight to some posts to override the default sorting (date descending)
---

Frozen depths is a singleplayer, narrative-driven puzzle game. Play as Dr. Fabio; a scientist in search of a cure for a strange illness plaguing the world. Discover a powerful tool and use it to melt and create ice throughout the vast caves of Antarctica.

{{< youtube Ki7QGZDyZ9Q >}}

**During this project, I was responsible for:**

- XYZ Chunking.
- Marching Cubes.
- Perlin Noise.
- Mesh Creating and Modifying in realtime.
- Unity Gizmos.
- Serialization.

My key role was to develop a system where you could create and melt ice.
To achieve this goal I decided that marching cubes would be the best way to approach the problem.

This project took 4 months to do in this project I experienced many bugs from ice not connecting to performance being almost a slide show.

I started by first making a basic terrain using a marching cube tutorial I followed online then started to implement an editing feature by grabbing points on the mesh by using the XYZ coordinates of the point hit on the mesh and then passing it into a function that could translate it into the array form, in turn, allowing me to increase or decrease the given point to simulate a melting or growing motion to the mesh.

After doing this I noticed that there was a huge performance hit as by doing this you would have to reload and create the entire mesh every time a point was edited, so to fix this issue I decided to chunk the entire mesh into 8x8x8 points, This worked but had the issue of the points near other chunks would not connect correctly to fix this problem I made the edge of each chunk be a reference to each other perpendicular chunk around it, this would basically mean that all surrounding chunks share edge points eliminating this bug.

For this mechanic to be usable for a designer with minimal programming experience I implemented a system that would grab all child objects and use them as a template of where the ice will be generated, as displayed in the image below.

{{< figure src="/frozen-depths-before-after.jpg" alt="Frozen Depths" caption="Frozen Depths Ice Blockout" >}}

To increase loading time between scenes I also added a serialization step that would check if the mesh had been made in the past or if a child object had been moved and if a child was moved or it was new it would cache itself for future use as loading from a file would tend to be quicker on larger meshes that contained a lot of children as it would not have to calculate anything or check any children for collisions, This would sometimes increase loading times by over 100%.

But even after all this there is still a bug I have yet to fix which is due to some surrounding chunks not updating after a neighboring chunk has been edited, this can be seen in the video below and could be fixed by double checking all neighbors are being updated.

<!--Youtube Vid-->
{{< youtube 3MWG3Pbg3GE >}}

The game is available to clone on [Github](https://github.com/AlexMollard/Frozen-Depths-Programmers).