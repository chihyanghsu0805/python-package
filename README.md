# python-package

## [Distutils](./distutils.md)

## [Setuptools](./setuptools.md)

https://setuptools.pypa.io/en/latest/userguide/quickstart.html#basic-use


When creating a Python package, you must provide a `pyproject.toml` file containing a build-system section similar to the example below:

```
[build-system]
requires = ["setuptools"]
build-backend = "setuptools.build_meta"
```

This section declares what are your build system dependencies, and which library will be used to actually do the packaging.

In addition to specifying a build system, you also will need to add some package information such as metadata, contents, dependencies, etc. This can be done in the same pyproject.toml file, or in a separated one: setup.cfg or setup.py.

-   [project](./project.md)
-   [package](./package.md)
