---
title: "Automated Folder Structure with TKinter & Python"
tags: [code, Auto, Automation, Py, python]
category: [code]
---

I like organizing my folder structure based on different applications & disciplines. Having a clear idea of what your a project structure looks like will ensure that files & assets don’t go missing. I’ve been messing a bit with paths and directories and found that this would be a great opportunity to work a little on some of those skills with Python. The goal of this was to write something that was quick and simple though not necessarily optimal but leave plenty of room to improve and oh boy, I succeeded in that last part pretty well.

This short script allows a user to generate a hierarchy of folders in a user-specified directory. It leverages tkinter for querying a directory in which to generate the project structure, and can be executed from a bat file for quicker access.

```python
import os
import tkinter as tk
from tkinter import filedialog
 
# Initializes tKinter widget window
root = tk.Tk()
root.withdraw()
 
# Ask the user for a directory
file_path = filedialog.askdirectory()
 
# List of parent folders
folders = ["houdini", "renders", "maya", "meshes", "references", "textures", "unreal"]
 
# Path to parent folders
houdini_dir = os.path.join((file_path + "/" + folders[0]))
textures_dir = os.path.join((file_path + "/" + folders[5]))
renders_dir = os.path.join((file_path + "/" + folders[1]))
 
# Sub-directories
houdini_folders = ["geo", "hda", "scripts", "tex"]
texture_folders = ["designer", "painter", "output", "mixer", "psd"]
renders_folder = ["wips", "finals", "marmoset"]
 
def make_project_dir():
    # Topline folders with sub-directories
    houdini_dir = os.path.join((file_path + "/" + folders[0]))
    textures_dir = os.path.join((file_path + "/" + folders[5]))
    renders_dir = os.path.join((file_path + "/" + folders[1]))
 
    # Create primary folders
    for f in folders:
        folder_path = os.path.join((file_path + "/" + f))
        try:
            os.mkdir(folder_path)
            print("Creating " + f + " folders...")
        except FileExistsError:
            print("Folder already exists!")
 
    # Create houdini sub-directories
    for hou in houdini_folders:
        houdini_sub_dir = os.path.join((houdini_dir + "/" + hou))
        try:
            os.mkdir(houdini_sub_dir)
            print("Creating " + hou + " folders...")
        except FileExistsError:
            print("Folder already exists!")
 
    # Create Texture sub-directories
    for tex in texture_folders:
        textures_sub_dir = os.path.join((textures_dir + "/" + tex))
        try:
            os.mkdir(textures_sub_dir)
            print("Creating " + tex + " folders...")
        except FileExistsError:
            print("Folder already exists!")
 
    # Create Render sub-directories
    for out in render_folders:
        renders_sub_dir = os.path.join((renders_dir + "/" + out))
        try:
            os.mkdir(renders_sub_dir)
            print("Creating " + out + " folders...")
        except FileExistsError:
            print("Folder already exists!")
 
 
make_project_dir()
```

I could have a template folder structure sitting in some bespoke location, but that wouldn’t have been fun. Also, it could easily be misplaced. It also means that if for any reason, there were a duplicate copy of that template, I would then have to figure out which one’s the outdated one. Cue many past mistakes calling out.

Let’s break it down a bit:

```python
root = tk.Tk()
root.withdraw()
```

We initialized tKinter which draws the main window. But we don’t want to use that widget as we’ll be instantiating the filedialog class. This means we need a way to hide that widget window. That’s where the withdraw() function comes in. The opposite to that is deiconify(), which lets you show a previously hidden widget.

```python
file_path = filedialog.askdirectory()
```
The next thing we want is the to query the root location in which we’re going to be generating our hierarchy which is pretty self explanatory.

```python
folders = ["houdini", "renders", "maya", "meshes", "references", "textures", "unreal"]
houdini_folders = ["geo", "hda", "scripts", "tex"]
texture_folders = ["designer", "painter", "output", "mixer", "psd"]
renders_folder = ["wips", "finals", "marmoset"]
```

Next comes the various folders & sub-directories that we want to create. Having separate lists for each collection of sub-directories seemed to make the most sense at the time but it makes it slightly difficult for expanding on options as that would require further adaptation of the code each time there were a new item required.

This also makes if we throw a fancy UI over the top of this, we use these as presets and even give power to the user to expand on each of these sub-directory lists.

```python
# Path to parent folders
houdini_dir = os.path.join((file_path + "/" + folders[0]))
textures_dir = os.path.join((file_path + "/" + folders[5]))
renders_dir = os.path.join((file_path + "/" + folders[1]))
```

It’s the same situation with the sub-directories, even more so. This is done in two stages. First, set the variables & paths for each of the parent folders that would contain sub-directories. Then create a series of lists for each of those relevant folders. Those lists will determine what those third level directories are.

```python
# Sub-directories
houdini_folders = ["geo", "hda", "scripts", "tex"]
texture_folders = ["designer", "painter", "output", "mixer", "psd"]
render_folders = ["wips", "finals", "marmoset"]
```
This by far isn’t a safe approach as should those indexes change positions, our sub-directories will end up in the wrong location and we’d be very sad about it. It also, as mentioned earlier, further restricts the feasibility of expanding on these directories.

It would be better if all of these lists were generated deterministically, maybe through an imported constants file or JSON dictionary, as opposed to a series of fixed list.

```python
def make_project_dir():
 
    # Create primary folders
    for f in folders:
        folder_path = os.path.join((file_path + "/" + f))
        try:
            os.mkdir(folder_path)
            print("Creating " + f + " folders...")
        except FileExistsError:
            print("Folder already exists!")
```

Next comes the main function body which is mostly the same code, but repeated for each of the different directories with two levels to them. Lots of repetition which we could reduce by wrapping inside a class and instantiating.

The idea is straight forward. For each item in the list, set a path any sub-directories, for each item in that list and wrap it in a try and except to catch if a folder already exists. If it already exists, do nothing.

One thing that this script hasn’t taken into account though is if the user bails out of the process. Should they hit cancel when prompted for a directory, the folders will still be created but at the drive root.

Ideally, the script would throw up either a confirmation box or finds a way to detect if a user has hit cancel.

```python
@echo off
python %~dp0\project_structure.py %*
pause
```

‘This last snippet is used to call on the script and run the process. For this bat file to work, the file must sit in the same location as the python file. In essence %~dp0 expands the search to the path of that bat file. It’s a really handy way of making batch files more portable and accessible.

Finally, one big plus from all of this is you can call on this bat file from a quick access tool such as DirectFolder or Listary and bind this bat file to a keystroke. Ultimately, that was what I was hoping to achieve from this and the script, while there’s a lot that can be improved has done it’s supposed so.