The following example demonstrates a minimum configuration (which assumes the project depends on requests and importlib-metadata to be able to run):

-   pyproject.toml

```
[project]
name = "mypackage"
version = "0.0.1"
dependencies = [
    "requests",
    'importlib-metadata; python_version<"3.8"',
]
```

-   setup.cfg

```
[metadata]
name = mypackage
version = 0.0.1

[options]
install_requires =
    requests
    importlib-metadata; python_version < "3.8"
```

-   setup.py

```
from setuptools import setup

setup(
    name='mypackage',
    version='0.0.1',
    install_requires=[
        'requests',
        'importlib-metadata; python_version == "3.8"',
    ],
)
```
