---
title: "Houdini Essentials 101"
tags: [proceduralism, houdini, gamedev, ゲーム開発, basics, 基本, 🔰初心者]
category: [gamedev]
---

# Houdini Context

Houdini uses different disciplines/contexts to separate out different types of nodes for different types or work. Think of the different departments/disiciplines required to creation a 3D image or animation. From a high level view, it can generally be broken down into these subcategories:

- Modelling
- Shading
- Rigging
- Animation
- Lighting
- Simulation
- Compositing
- Rendering

For each of these disciplines, Houdini has nodes that work within these specific areas. Houdini takes these concepts and compartmentalizes them into different contexts. In Maya, this would be the same as different Shelf Toolsets. Each node type/context in Houdini is described as an operator.

## 1. Navigation & Viewport handles

Objects sit at the top level of every scene. Each session or Houdini scene is comprised of a series of objects, arranged in certain ways to create an image. A geometry network at the object level holds geometry or SOP nodes inside that network.  A GEO network is comprised of a series of SOP nodes or Surface operators to create/manipulate surface data by wiring those nodes together. Different surface operators. such as Bevel, Extrude & UV Edits are performed within this context.

## 2. Quickviews, Construction Planes & Quickplanes

Like most other nodes flows in Houdini, COP nodes flow from top to bottom. Drag a node into the viewer to view that node's output. COP's can be used to either generate or manipulate texture images.  In short it's a compositing tool for processing 2D images. However, data can be streamed in from other context, processed within COP's and fed back into those other context.

## 3. Snapping

Anything related to the exporting or rendering of data. ROPs establish rendering dependency networks. Houdini's default render is Mantra. Other popular third-party renderers include Renderman, Redshift & Octane.

Recently SideFX introduced a new more powerful renderer called Karma as part of their Solaris toolset. As a result, Karma is found under a LOPs network due to it's ties with the USD system.

## 4. Directories & Network Managers

Everything related to material creation. MAT contexts describes shading & material dependencies that will get applied to a geometry node. MAT's and VOP's are slightly different. MATs describe the final look and surface properties of a material. VOP's create the actual shader network that defines how a material works.

Each material or MAT network at it's core is essentially a VOP network. Nodes are connected together in VOP's which are then compiled into executable VEX code. VOP's are more than just materials however. VOP's is similiar to Unreal's Material Editor, Maya's Hypershade or Softimage XSI's ICE.

## 5. Quickmarks & Bookmarks

Known as Channel Operators. CHOP's are used for manipulating time-based channel data. Commonly used in combination with VOPs and SOPs for motion graphics. Can also be used for manipulating & processing audio files. Animation or particles can be affected by audio files spawned/loaded in CHOPs.

CHOPs are also in rigging and establishing character constraints. Aim constraints, euler rotations, inverse kinematics. These can all be handled within CHOPs.

- CHOP (Channel Operator)
- Time based channel data motion & audio
- Procedural anims
- Edit & Process Audio Files
- Constraints & Rigging

## 6. Creating Geometry

Contains nodes that create or affect information relating to the simulation and dynamics of particles, soft body physics & rigid bodies. DOPs are an FX artists toolbox, whether they are trying to create crowd motion, fire, smoke or white-water effects. POP's are a subset of DOP's which are specifically related to particle manipulation.

## 7. Geometry Components

Forms the core of Houdini's PDG system. At it's core, TOP networks are an elaborate task runner that can be used to automate tasks & speed up workflows. Commonly run tasks & jobs can be scheduled with Tractor or performed in parallel through a series of processors known as a Work Item.

- PDG (Procedural Dependency Graph)
- TOP (Task Operators)
- Dependency Networks to Automate Tasks
- New and Improved version of the ROP Context
- Run tasks in Parellel
- Automation Tools

## 8. Connecting Points

Nodes for working with USD data, describing character, props, lighting & rendering. Stands for Lighting Operators

- LOP (Lighting Operator)
- Is used for more than just lighting
- Houdini's Universal Scene Description context
- Procedural Hierarchy editor
- Lighting Operator is misleading as it's more of a layout/layer operator

## 9. VEX

Houdini's internal scripting language. Based in C, VEX borrows ideas from C++ & RSL and is commonly used to either extend Houdini or build complex networks and systems programmatically. Custom nodes and operators can be written in VEX. Data wrangling within Houdini is also commonly done in VEX. It's not however a replacement or alternative to traditional scripting. Houdini supports Python which is more commonly used instead of VEX to extend Houdini's UI.

Houdini supports a third scripting language in hscript. Hscript is also commonly used to extend Houdini's UI or writing more high level expressions. It's popularity and usage seems to be waning slightly however in recent times.

- VOP (VEX Operator)
- Build VEX Code Using Nodes
- Vector Expression Language
- Material Context is a VOP Network
- Build Custom Operators for Other Contexts
- Use VOPS and VEX to Extend Houdini
