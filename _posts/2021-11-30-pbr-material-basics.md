---
title: "PBR Material Basics"
tags:
  - pbr
  - shading
  - materials
  - textures
  - rendering
  - basics
  - 基本
  - 🔰初心者
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

## 2. PBR Basics

- Physically Based Rendering
- Rendering strategy to accurately describe the surface properties of an object.
- Previous rendering strategy attempted to imitate the appearance of lighting
- Makes graphic look more real
- PBR attempts to model light's behaviour
- Consists of two components: **Light Properties** & **Surface Properties**
- Light Properties:
  - Direct Diffuse
    - Light coming directly from light source
    - Scattered in all directions after hitting the surface
    - Computer with simple math in the shader
  - Indirect diffuse
    - Light coming from all directions in the environment
    - Scattered in all directions
    - Computer with GI solution, often rendered offline and baked into maps
  - Direct specular
    - Light coming directly from the source
    - Reflected in a more focused direction
    - Reflection of the light source
  - Indirect specular
    - Light coming from all directions
    - Reflected in a more focused direction
    - Computed using reflection probes,
    - Planar reflections, SSR or Ray Tracing
  - Shadows
  - Ambient Occlusion
- Surface Properties:
  - Base Colour
    - Defines albedo colour of the surface
    - Should not have lighting information/shadows baked in, purely colour info
    - Never darker than 20 sRGB
    - Never brighter than 240 sRGB
    - Rough surfaces have a higher in ~50 sRGB
    - Out of range values will not light correctly
    - Should be rather flat
    - Use real-world measurements or captured data for best result
  - Normal
    - Defines the shape of the surface
    - Each pixel channel represents a vector that indicates the direction that the surface is facing
    - Even when the mesh is perfectly flat, a normal map can make the surface appear bumpy/textured
    - Used to add surface detail that is otherwise impossible to expensive to compute
    - Should never be hand-authored
  - Specular
    - A multiplier for direct & indirect specular lighting
    - Defines the reflectivity when looking straight at the surface
    - Non-metal surfaces reflect about ~4% of light
    - 0.5 represents 4% of reflected light.
    - 1.0% represents 8% - too high for most objects.
    - At glancing angles, most surfaces are 100% reflection.
    - Change in surface reflections when viewing at different angles is due to fresnel which is everywhere.
    - Specular maps should be mostly at 0.5
    - Only darker shades to mask areas that should not be reflective - like crevices.
    - A crevice map multiplied by 0.5 makes a good specular map.
    - Taking a cavity map and multiplying it over the top on an ambient occlusion make might be a good way to get a good specular map
  - Roughness
    - Represents the roughness  of a surface at microscopic scale.
    - White is rough, black is smooth.
    - Controls the focus of the reflections.
    - Smooth = tight & sharp reflections
    - Rough = blurry & diffused reflections
  - Metallic
    - Two shaders in one. Metallic defines the metalicity of a surface.
    - White is full metal. Black is none metallic.
    - When set to full metal, the base colour in turn represents the reflectance value of a surface.
    - There's no such thing as dark metal.
    - Specular ranges for metallic surfaces is somewhere between 60%-100%. 100% representing the reflectance values of  chrome/mirror like surfaces.
    - Be sure to use real-world measurements for metal colour values and keep them bright.
    - [https://docs.blender.org/manual/en/latest/render/shader_nodes/shader/principled.html#examples](https://docs.blender.org/manual/en/latest/render/shader_nodes/shader/principled.html#examples)
    - [http://technicalartadventures.blogspot.com/search/label/PBR](http://technicalartadventures.blogspot.com/search/label/PBR)
    - Specular input is ignored when Metallic is 1
- Incoming light
  - Direct
  - Indirect
- Outgoing light:
  - Specular
  - Diffuse
- Four Light Types:
  - Direct diffuse
  - Direct specular
  - Indirect diffuse
  - Indirect specular

## 3. Data Types

| PLACEHOLDER |

## 4. Distortion Shader

- Use sort priorities
- Break large common tasks into material functions
- Comment your graph node
- Colour code your comments
- Use the reroute nodes
- Use material parameter collections
- Use separators

## 5. Flipbook Animation

| PLACEHOLDER |

## 6. Environment Blending

Custom material functions:

- mf_standard
- mf_mro
- mf_uv
- mf_texture_input
- mf_pom
- mf_tessellation
- mf_displacement
- mf_bump_offset
- mf_vertex_blend_layer
- mf_vertex_blend
- mf_grass_layer
- mf_edge_wear
- mf_slope_detection
- mf_camera_distance
- mf_fog
