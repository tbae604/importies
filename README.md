# importies

## About

This is a gist on Python imports because I still get confused sometimes.

Borrowed heavily from https://realpython.com/absolute-vs-relative-python-imports/

These should be compatible in both Python 2 and 3 because we're not using implicit relative imports (i.e. assumptions about current dirs).

PEP8 style guides recommend absolute imports but permit explicit relative imports if they provide better readability.

Current folder structure and key contents:

```
src
└-- folder1
|   |-- __init__.py
|   |-- module1.py
|   └-- module2.py      # def function1
└-- package2
    |-- __init__.py     # class class1
    |-- module3.py
    └-- subfolder1
        └-- module5.py  # def function2
```

## Definitions

A **module** is as simple as a *.py file – let's say mod.py. In an appropriate location, mod.py's contents can be accessed in-code/shell by `import mod` then e.g. `mod.some_list`, `mod.foo('abc')`, etc. The Python interpreter looks for mod in the current directory, dirs set in PYTHONPATH, or an installation-dependent list of dirs from when Python was installed. All three of these make up the search path, which is accessible via `sys.path` if you wanted to have a peek. Once imported, we can access `mod.__file__` to get its path.

A **package** is a folder of modules plus an __init__.py file – let's say in a folder named pkg as shown below. (This is not required in Python3 but imo is still good for consistency.) Following `import pkg`, the namespace would have the list A available to it. A convenient use is for __init__.py to `import pkg.mod1, pkg.mod2` inside it so that `import pkg` then gives access to the mods' contents as `pkg.mod1.foo()`, etc. This is better practice than say from `pkg import *`.

```
pkg
└-- __init__.py  # contains A = ['a', 'b', 'c']
    |-- mod1.py
    └-- mod2.py
```

A **subpackage** is a package within another package (see below).

If mod3 wanted to access `foo()` in mod1, we could use an absolute import: `from pkg.sub_pkg1.mod1 import foo`.

Or, an explicit relative import: `from ..sub_pkg1 import foo`. The two dots refers to the package from one level up (pkg).

```
pkg
└-- sub_pkg1
|   |-- __init__.py
|   |-- mod1.py        # def foo()
|   └-- mod2.py
└-- sub_pkg2
    |-- __init__.py
    |-- mod3.py
    └-- mod4.py
```
