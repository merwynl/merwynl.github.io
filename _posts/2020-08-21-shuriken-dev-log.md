---
title: "Shuriken Toolkit Dev Log 0.0.1"
tags: [code, Auto, Automation, Py, Tkinter]
category: [code]
---

For a while, I’ve been searching for a way to speed up my own personal workflow. Hotkeys and shortcuts are great but sometimes you might want to just click away if certain tools are close enough within reach. Plus there’s only so many tools you can quickly hotkey. Jumping back and forth between different DCC’s also means having to recall a lot of different hotkeys. That’s not a bad thing but someone just starting out may find, having to remember dozens and dozens of different hotkeys to be a little overwhelming.

One of the big reasons why I really like Maya’s Shelves system, It makes it really easy to customize and have quick access to a bunch of commonly used tools without having to context switch eternally in your mind. However it can be limiting because of the amount of ui real-estate a shelf can take up.

A couple of months back I started work on a custom toolset called Shuriken (name is placeholder for the moment) but I have been hesitant to talk about it because it’s still it’s very early stages of development. The inspiration for this tool comes off the back of using some really great one’s such as [froTools][frotools] and MJPolyTools.

I’ve been developing the tool as a means to get more comfortable with Maya’s Python API but it also provided an opportunity to build something that could maybe someday be used in a much wider context.

The aim of this toolset is for quick and easy access to some of the most common tools that I use on a daily basis as well as a couple of custom one’s for faster iterations.

I originally went with Maya Commands because I had heard about some of it’s benefits and wanted to experiment with it for a bit. I may switch back to Maya Commands if the tool starts to slow down a bit but currently I’m treating this as a learning experiment.

This page has a pretty good breakdown of Maya’s Python API as well as some speed benchmarks. There’s not much point in me running a speed test on the Shuriken toolkit until more functionality has been included. Right now, the speed difference isn’t noticeable.

The next thing I decided on was how I was going to frontload the UI. I knew I wanted it to be dockable. If there’s one thing I really dislike a lot of, it’s having too many floating windows. It also has to be somewhat scalable if I decided that more tools and functions were to be added further down the line.

PySide sounded like a good option. It’s widely used, has native support in Maya and allows for custom UI files from QtDesigner, which, the arty part of me was really looking into. However I hadn’t yet had much experience writing with Qt, let alone building fancy UI’s through widgets and stylesheets. I’ve been exposed to a bunch of the concepts at work but for Shuriken it feels a little overkill and unnecessary.

I came across a command called workspaceControl. It was introduced back in Maya 2017 and provided a way to dock custom Qt widgets in Maya by invoking UI files through the uiScript flag. But it’s not necessary to use designer UI files. Their docs states that you can have your UI under a separate function and then call that function in your invoke.

Here’s an example:
```python
import pymel.core as pm
 
if pm.workspaceControl("Window", exists =True):
    pm.deleteUI("Window")
 
def UI(*args):
    # Main Column layout
    pm.columnLayout(adj = True, w=250, h=805)   
 
    # Primitive Layout
    primitives_layout = pm.columnLayout(adj =True)
 
    # Buttons for creating primitives
    create_sphere_button = pm.button( label= "Sphere")
    create_cube_button = pm.button( label= "CubeCube ")
     
    pm.setParent(primitives_layout)
 
pm.workspaceControl("Window", retain=False, floating=True, uiScript="UI()")
```


I’m not using a separate UI file as I didn’t want to have to manage another file if I didn’t have to. However, if this tool ever gets big enough where I have to split it up into more separate modules then I might revisit the idea then. The above solution sits my current needs.

There are a couple more great examples [here][here].

[Kaine van Germet][Kaine van Germet] offers a much more in-depth dissection on how to use Workspace Controls with standard Qt layouts to create dockable windows. I opted to use Maya layouts instead as my needs here are far simpler.

Should I decide that this tool becomes useful enough to be released, I’ll consider using a more traditional software development approach for handling these dev logs. For now, I might continue with releasing updates in this format.


[frotools]: https://www.froyok.fr/assets/frotools/
[here]: https://python.hotexamples.com/examples/maya.cmds/-/workspaceControl/python-workspacecontrol-function-examples.html
[Kaine van Germet]: https://kainev.com/qt-for-maya-dockable-windows/