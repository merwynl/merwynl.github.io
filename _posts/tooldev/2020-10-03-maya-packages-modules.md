---
title: "Importing Modules & Package Scripts in Maya"
tags: [code, Auto, Automation, Py]
category: [code]
---

Importing & running external scripts is a key component in making scripts portable. Splitting your scripts into separate files is a convenient way of breaking a part large chunks of code & functionality into smaller pieces. Each separate python file that created is a module and a package is a collection of module/s.

The idea of a Python package looks something like this:

```python
/bin
main.py
    /package
    __init__.py
    module_1.py
    module_2.py
```

Here’s an example of importing & running a Python script inside Maya. Say we have a module called my_module.py and it has a bunch of functions like so:

```python
import maya.cmds as cmds
 
# Function that does stuff
def MakeCube():
    cmds.polySphere()
    print('Sphere made!')
```

This module currently lives in a package in maya\version\scripts\package and we want to import & run this script from inside Maya. This snippet already shows us importing the Maya Commands module that gives us access to the polySphere() function.

If the script was living inside the scripts folder and not one extra level down, we could do something like this:

```python
import my_module
reload(my_module)
my_module.MakeCube()
```

The reload function ensures that we are always in sync what we’re importing. As we did with importing Maya Commands, we can do the same here with our own module which reduces the amount of typing in our code like so:

```python
import my_module as md
reload(md)
md.MakeCube()
```

Because in this instance our module is sitting in its own packages under the scripts folder, Maya has no knowledge of that path. We can figure out the paths that Maya is currently aware of by using the python sys module:

```python
 
for path in sys.path:
    print path
```

If we run this in Maya’s script editor, we can see a list of paths that Maya automatically recognizes. We can extend this and add our package path to this sys, either by appending to this list with the sys.path.append() function, which will have to be done for each new session of Maya, or we can add the path through a variable in the Maya.env file. We could even create a .mod file with the absolute path and add that file to the maya\version\modules folder. This is one of the ways in which Maya handles the distribution of different plug-in modules.

Depending on your requirements, either of these options is a viable solution. However, if your script is relatively straightforward and consists of either a single python module or package, it’s better to avoid unnecessary complexities & to store your scripts in a package or path that Maya sees and import it from there.

Going back to our original issue however, we can’t just do a straight import. As stated previously, Maya has no knowledge of the package path. And we can do a sys.path.append() which would be the go to method if your packages live somewhere else. In our case however, we can still read the package using Python’s from method because it lives inside a path that Maya has access to. We can do something like this:

```python
from package import my_module as module
reload(module)
module.makeCube()
```

Here, we’re importing our module from the package, reloading it to ensure that we are syncing the Maya interpreter with the latest module and then running the function.

If our function call was inside the module then importing & reloading the script would have been more than enough. However, you may find that may sometimes want control over when to call on a function or if you have multiple functions, determine which function you want to call.

Your module may also have a number of classes and you may simple want to instantiate that a class of MainClass, in which case the above approach is more appropriate.

We could also add a few safety checks around our function call, either by wrapping it in a try & except

```python
from package import my_module as module
import maya.OpenMaya as om
 
 
# Attempts to reload the module & run a function
try:
    reload(module)
    om.MGlobal.displayInfo('Module Reloaded')
    module.makeCube()
except NameError:
    om.MGlobal.displayWarning('Incorrect module name!')
except ImportError:
    om.MGlobal.displayWarning('Failed to import module!')
```

or by writing a separate function that check if the module has been successfully reloaded:

```python
from package import my_module as module
import maya.OpenMaya as om
 
 
# Reload the module & run a function
def RunExternalFunction():
    if reload(module):
        om.MGlobal.displayInfo('Module Reloaded')
        module.makeCube()
    else:
        om.MGlobal.displayWarning('Failed to execute function')
 
RunExternalFunction()
```


Here, we’re also making use of the OpenMaya API to display some info to the status bar if the import has failed.

This is overkill for something simple but hopefully it’s provided some useful information.