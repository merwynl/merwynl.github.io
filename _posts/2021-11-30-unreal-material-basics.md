---
title: "Material Basics in Unreal"
tags: [pbr, shading, materials, textures, rendering, basics, 基本, 🔰初心者]
category: [shaders, gamedev, unreal, ゲーム開発]
---

# Material Basics

- **Textures Sampler Source**: Shared allows the use of more than 16 texture samplers.
- **Texture Objects** - Stores a reference to a texture but does not actually sample it.
- **Texture Sampler**: Gets a references to a texture and samples it based on UV coordinates.
- **Const Coordinate** - Same as setting the Coordinate Index on a Texture Coordinate node.
- **Sampler Type** - Differs depending on the texture compression type. Usually set automatically but can be overwritten.
- **Fully Rough** - Ignores roughness property and sets it to be always rough. Optimizes the number of instructions and sampler count.
- **Normal Curvature to Roughness** - Good for metallic & clear coat materials. Reduces roughness based on screen space normal changes.
- **IsSky**  - Meshes with a material that has this enabled will not receive any skylight contribution. Height & Volumetric fog will remain.
- **SSR** - Enables SSR on a per material basis.
- **Contact Shadows** - Allows for contact shadows on translucent objects.
- **Compute Fog Per Pixel** - Reducing artefacting on material surfaces that intersect with fog elements. A bit more expensive.
- **Render After DOF** - Allows for translucency to be rendered in a separate pass. Requires Separate Translucency Enabled in project Settings.
- **Tessellation Mode** - Two different methods of calculating tessellation.
- **Flat Tessellation**  - Splits up the triangles but doesn't do anything else to it.
- **PN Triangles** - Splits & smooths the objects. Objects in question required smoothing groups.

## 1. Common Nodes

- **3 Vector** - 3 channel node without alpha.
- **4 Vector** - 3 channel node with a separate alpha channel.
- **Lerp** - Linear Interpolate used for blending two inputs by an alpha.
- **Divide** - When applied to numbers divides them. When applied to textures Darkens them.
- **Add** - When applied to numbers adds them. When applied to textures Lightens them. Adding  a value to a texture coordinate node has the ability to shift the uv's in x or y.
- **Multiple** - When applied to numbers multiplies them.  When applied to textures Multiplies them.
- **SetMaterialAttributes** - Similar to MakeMaterialAttrs but it lets you choose specific attrs.
- **WorldAlignedTexture** - Projects textures in WorldSpace rather than relying on UV's
- **Static Bool** - Good to hide/show features from material instances
- **Flatten Normal** - Flattens a normal input

## 2. Material Basics

**Textures Sampler Source**: Shared allows the use of more than 16 texture samplers.

**Texture Objects** - Stores a reference to a texture but does not actually sample it.

**Texture Sampler**: Gets a references to a texture and samples it based on UV coordinates.

**Const Coordinate** - Same as setting the Coordinate Index on a Texture Coordinate node.

**Sampler Type** - Differs depending on the texture compression type. Usually set automatically but can be overwritten. 

**Fully Rough** - Ignores roughness property and sets it to be always rough. Optimizes the number of instructions and sampler count.

**Normal Curvature to Roughness** - Good for metallic & clear coat materials. Reduces roughness based on screen space normal changes.

**IsSky**  - Meshes with a material that has this enabled will not receive any skylight contribution. Height & Volumetric fog will remain.

**SSR** - Enables SSR on a per material basis.

**Contact Shadows** - Allows for contact shadows on translucent objects.

**Compute Fog Per Pixel** - Reducing artefacting on material surfaces that intersect with fog elements. A bit more expensive.

**Render After DOF** - Allows for translucency to be rendered in a separate pass. Requires Separate Translucency Enabled in project Settings.

**Tessellation Mode** - Two different methods of calculating tessellation.

**Flat Tessellation**  - Splits up the triangles but doesn't do anything else to it.

**PN Triangles** - Splits & smooths the objects. Objects in question required smoothing groups.

## 3. Material Types

Default Lit
Translucent
Unlit
Masked
TwoSided Foliage
Thin Translucency
Single Layer Water

## 4. Organizing your Material Graphs

- Use sort priorities
- Break large common tasks into material functions
- Comment your graph node
- Colour code your comments
- Use the reroute nodes
- Use material parameter collections
- Use separators