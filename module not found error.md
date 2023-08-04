Resources:
- [what is __init__.py for?](https://betterstack.com/community/questions/what-is-init-py-for/)

> TLDR: Module not found error typically arises when the python interpreter cannot find the module/ package that you are attempting to import.

Given an example directory
```python
.
└── project
    └── src
        ├── main.py
        └── model
            ├── __init__.py
            └── mypackage.py
```

Attempt:
```
import mypackage
```
> Error: `ModuleNotFoundError`

Fix
1. Check `sys.path`, and ensure that the absolute path to the workspace directory `{path_to}/project` is seen - e.g., `[...'/hdd4/jiet/code/project']`.
```
import sys
print(sys.path)
```
> `sys.path` - a list that contains the directories where the Python interpreter searches for modules to import

2. If path to workspace directory is not seen, ***add path to workspace directory manually*** using `sys.path.append()`/ `sys.path.insert()`
```
import sys

# Converts relative path to absolute path
sys.path.append(os.path.abspath('{relative_path}'))
```
OR
```
import sys

sys.path.append('{absolute_path}')
```
> Depend on how you `import`  modules, you might need to reveal different absolute paths to `sys.path` to make the warnings go away.

3. Import the nested module 
```
import model.mypackage
```
OR
```
from model.mypackage import Class_name
```


