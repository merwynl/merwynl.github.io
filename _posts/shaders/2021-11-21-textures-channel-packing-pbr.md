---
title: "Notes on Textures & PBR"
tags: [pbr, shading, materials, textures, rendering, basics, 基本, 🔰初心者]
category: [gamedev]
---

### Channel Packing Textures

- TextureName_ALB.tga
  - Albedo map
- TextureName_NORM.tga
  - Normal map
- TextureName_ORM.tga
  - O = Occlusion
  - R = Roughness
  - M =Metallic

### Acronyms

PBR = Physically Based Rendering
- Rendering & Lighting Concepts

PBS = Physically Based Shading
- Shading Concepts

### PBR Theory

Both PBR & PBS refers to representing assets in a physically accurate context

- Ensures using accurate albedo colours & reflectance values
- Will look physically accurate in all types of lighting conditions
- Ensures consistency with material definitions

3 different tents for understanding PBR:

### Energy Conversation

- Total amount of reflected light will never be more than the incident/incoming light
- Diffuse/rough surface will reflect a very dim and wide highlight
- Smoother & glossier will reflect tighter & brighter highlights
- An object cannot generate its own light

### BRDF (Bi-directional reflectance distribution function)

- A mathematical function that describes the reflective properties of a surface
- Many different BRDF's exist
  - Disney's BRDF (Modification of the GGX BRDF)
  - GGX
  - Cook-Torrance
  - Oren-Nayar
  - Lambertian
  - Blinn-Phong
  - Phong (Not to be confused with Blinn-Phong)
  - Ward
  - UE4 uses GGX

### Conductive vs Dielectric materials

- Dielectric
  - Are insulators
  - Absorb more than they reflect
  - Absorb electricity
  - Examples include plastic, rubber, ice, glass, rusted metal
  - Generally anything non-metal
- Conductive
  - Conduct electricity
  - Generally includes all metals
  - Does not include rusted metals

2 different workflows for handling these materials:

- Gloss/Spec
- Metalness/Roughness

Unreal uses Metalness/Roughness

### Metalness/Roughness

- Generally more cost effective than Gloss Spec and easier for artists to understand & interpret
- Allows channel packing
- Albedo should contain no lighting information / AO
- In a Metalness/Roughnes workflow, you technically can inject colour into the metallic channel but it's simpler and more accurate to keep Metalness to black and white and injest the colour into the albedo channel.
- AO may sometimes be included into the albedo for certain foliage but should only ever be used for micro/macro details
- Metalness
  - Black / 0.0 = Non-metal
  - White/ 1.0 = Full metal
  - Values cannot exceed past 1
  - You can sometimes use grey values for transitional materials such as rust and certain dirt
  - It is not recommended not to have a sharp contrast between black to white because it may cause rendering issues with the transitional materials
  - Essentially this means that if you have a black & white mask for your metalness maps, the transition area from black to white/vice versa should consist of some feathered areas of grey to represent those transitions

### Gloss/Spec

- If using Gloss/Spec to create anything metallic, you would have to use the colour from the specular channel
- There will never be an all black specular map
- For specular values, everything will have a minimum grey value
- Gloss/Spec runs the opposite of Metalness/Roughness
- Gloss
  - Black/0.1 = Less shiny / Non-metal
  - White/1.0 = Shiny plastic / metal
  - At full gloss, a material will have tighter & brighter highlights
  - In the opposite, the highlights & reflections will be broader & more diffused
- Specular
  - Black / 0.0 = Less reflective
  - White / 1.0 = More reflective
- To achieve a mirror like surface, both Gloss & spec have to be at 1
- Albedo does not contribute to Gloss/Spec
- Coloured metals should have the hues adjusted within the specular channel.
