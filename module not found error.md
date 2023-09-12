Resources:
- [what is __init__.py for?](https://betterstack.com/community/questions/what-is-init-py-for/)
- [Neural nine: Importing your own python modules properly](https://www.youtube.com/watch?v=GxCXiSkm6no)

> TLDR: Module not found error typically arises when the python interpreter cannot find the module/ package that you are attempting to import.

Preamble:
- **module**: a single file containing Python code. It can define functions, classes, variables, and other objects.
- **package**: a collection of Python modules.

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
1. Add a `__init__.py` file is a special file that is used to define a directory as a ***package***. 
	- Creating an empty `__init__.py` already tells python `.py` files within the directory (package) are ***modules***.
	- Code written in `__init__.py` file will be *executed when the package is imported*. This is useful for any package-level setup, initialization, or configuration that needs to happen.
 Things you can do in the `__init__.py` file:
```__init__.py
# Create a global variable that will be accessible using: mypackage.module1.my_variable  
my_variable = 42

# List the names of the modules within package 
__all__ = ['module1', 'module2']
```
2. Check `sys.path`, and ensure that the absolute path to the workspace directory `{path_to}/project` is seen - e.g., `[...'/hdd4/jiet/code/project']`.
```
import sys
print(sys.path)
```
> `sys.path` - a list that contains the directories where the Python interpreter searches for modules to import

3. If path to workspace directory is not seen, ***add path to workspace directory manually*** using `sys.path.append()`/ `sys.path.insert()`
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

4. Import the nested module 
> Usually, `model` is a directory, `mypackage` is a python file. So be sure to not make a mistake to only import `import model` or `import mypackage` after including it to `sys.path`.
```
import model.mypackage
```
OR (if the `mypackage.py` has a Class data structure)
```
from model.mypackage import Class_name
```

5. Last resort
> Check if your graphviz is install in the correct kernel/ python interpreter that runs your code/ jupyter notebook. If there are at different locations, the import will not be successful.

- Check if your machine uses correct python interpreter by default
```
where python
```
- You should expect something like: `.../anaconda3/.../python`

> If anaconda python is not used by default, you have to add `export` commands into your `$PATH` variable manually in the terminal script(e.g., at the last line of `~/.zshrc`/ `~/.bashrc`).
```
export PATH="/path/to/your/home/anaconda3/bin:$PATH"
```

OR

> If you are running a jupyter notebook, python interpreters are bound to your jupyter kernel's associated python version.

- Create a new ipykernel, while specifying python version
 $ `python{version} -m ipykernel install --user --name=<kernel-name>`
