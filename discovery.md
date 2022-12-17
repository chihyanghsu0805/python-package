Normally, you would specify the packages to be included manually in the following manner:

-   pyproject.toml

```
# ...
[tool.setuptools]
packages = ["mypkg", "mypkg.subpkg1", "mypkg.subpkg2"]
# ...
```

If your packages are not in the root of the repository or do not correspond exactly to the directory structure, you also need to configure package_dir:

-   pyproject.toml

```
[tool.setuptools]
# ...
package-dir = {"" = "src"}
    # directory containing all the packages (e.g.  src/mypkg1, src/mypkg2)

# OR

[tool.setuptools.package-dir]
mypkg = "lib"
# mypkg.module corresponds to lib/module.py
"mypkg.subpkg1" = "lib1"
# mypkg.subpkg1.module1 corresponds to lib1/module1.py
"mypkg.subpkg2" = "lib2"
# mypkg.subpkg2.module2 corresponds to lib2/module2.py
# ...
```
