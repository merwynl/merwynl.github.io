---
title: "Intro to Gaea"
tags: [proceduralism, houdini, gamedev, ゲーム開発, basics, 基本, 🔰初心者]
category: [gamedev]
---

# Introduction to Gaea

Node based terrain system. Can be buggy and prone to stability issues.

## 1. UI

If you see an opportunity where user research would substantially help us develop a product or feature, start by writing a proposal in the Docs database.

**Toolbox**

- Contains all terrain nodes
- Has two modes, Standard & Expert, which hides/shows categories of nodes.
- Slider on the top right toggles to commonly used nodes.
- Position can be changed between Right, Bottom & Full.
- Nodes can also be accessed from the Graph using the Tab key

**Graph**

- Main work area
- Has several different node styles which cab be changed in the Preferences.
- Multiple graphs can be created & colour coded
- 'Mark for Export' marks a node for export

**Properties**

- Adjust the properties for each node

**Control keys**

- U - In graph view to toggle mask view mode
- F6 - In graph view to toggle 2D view
- Alt + Left Mouse  - Rotate
- Middle Mouse - Pan
- Mouse Wheel - Zoom
- F4 - Auto Layout Nodes
- Ctrl + R - Reset current node properties
- F8 - Mixes 2 or more nodes together, same as laying down a Combine node
- Rotating the viewport is fixed to the centre of the world.

## 2. Nodes

**Mountain**

- Create a basic mountain
- Edge - pushes the mountain down, creating a circular crater
- Seed - Variants of the mountains
- Shape Style - Switch between classic & dune style mountain

**Voronoi**

- Create procedural noise
- Enable dual for dual voronoi
- If using high scale values, can be clamped to never exceed past a certain threshold
- Warp can be used to warp the noise. Useful for creating magma flows at higher warp frequency.

**Voronoi+**

- Completely different to standard voronoi
- Can be used to create cragly rocks similar to the Giant's Causeway.

**Slope Noise**

- Noise on a slope
- Stratified - Useful for making terrace like cragly terrains

**Plates**

- Strong profile with lot of directionality

**Draw**

- Allows for custom shapes to be drawn

**Igneous**

- Large mountains with a lot of soft canyons & underlays.
- Can be used with the clamp to reduce noise influence

**Heal**

- Works similar to denoise
- Attempts to softens a lot of high frequency noise but keeps the high peaks
- Blue node blurs everything
