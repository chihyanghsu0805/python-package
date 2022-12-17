https://docs.python.org/3/distutils/introduction.html#a-simple-example

If all you want to do is distribute a module called foo, contained in a file foo.py, then your setup script can be as simple as this:

```
setup(
    name="foo",
    version="1.0",
    py_modules=["foo"]
)
```

-   modules are specified by module name, not filename (the same will hold true for packages and extensions)

To create a `source distribution` for this module, you would create a setup script, setup.py, containing the above code, and run this command from a terminal:

```python setup.py sdist```

sdist will create an archive file (e.g., tarball on Unix, ZIP file on Windows) containing your setup script setup.py, and your module foo.py. The archive file will be named foo-1.0.tar.gz (or .zip), and will unpack into a directory foo-1.0.

If an end-user wishes to install your foo module, all they have to do is download foo-1.0.tar.gz (or .zip), unpack it, and—from the foo-1.0 directory—run

```python setup.py install```

which will ultimately copy foo.py to the appropriate directory for third-party modules in their Python installation.

This simple example demonstrates some fundamental concepts of the Distutils. First, both developers and installers have the same basic user interface, i.e. the setup script. The difference is which Distutils commands they use: the sdist command is almost exclusively for module developers, while install is more often for installers (although most developers will want to install their own code occasionally).

https://docs.python.org/3/distutils/setupscript.html#listing-whole-packages

The packages option tells the Distutils to process (build, distribute, install, etc.) all pure Python modules found in each package mentioned in the packages list. In order to do this, of course, there has to be a correspondence between package names and directories in the filesystem. The default correspondence is the most obvious one, i.e. package distutils is found in the directory distutils relative to the distribution root. Thus, when you say packages = ['foo'] in your setup script, you are promising that the Distutils will find a file foo/__init__.py (which might be spelled differently on your system, but you get the idea) `relative to the directory where your setup script lives`. If you break this promise, the Distutils will issue a warning but still process the broken package anyway.

```
setup(
    name="bar",
    version="1.0",
    packages=["bar"],
)
```

https://docs.python.org/3/distutils/setupscript.html#listing-individual-modules

For a small module distribution, you might prefer to list all modules rather than listing packages—especially the case of a single module that goes in the “root package” (i.e., no package at all). This simplest case was shown in section A Simple Example; here is a slightly more involved example:

```
setup(
    name="foo_bar",
    version="1.0",
    py_modules=["foo", "bar.bar"],
)
```

This describes two modules, one of them in the “root” package, the other in the pkg package. Again, the default package/directory layout implies that these two modules can be found in mod1.py and pkg/mod2.py, and that pkg/__init__.py exists as well. And again, you can override the package/directory correspondence using the package_dir option.

https://docs.python.org/3/distutils/builtdist.html#creating-built-distributions

A `built distribution` is what you’re probably used to thinking of either as a `binary package` or an `installer` (depending on your background). It’s not necessarily binary, though, because it might contain only Python source code and/or byte-code; and we don’t call it a package, because that word is already spoken for in Python. (And “installer” is a term specific to the world of mainstream desktop systems.)

``` python setup.py bdist ```

https://docs.python.org/3/distutils/examples.html#distutils-examples

More typically, though, you will want to distribute multiple modules in the same package (or in sub-packages). For example, if the foo and bar modules belong in package foobar, one way to layout your source tree is

<root>/
    setup.py
    foobar/
        __init__.py
        foo.py
        bar.py

This is in fact the default layout expected by the Distutils, and the one that requires the least work to describe in your setup script:

```
setup(
    name='foobar',
    version='1.0',
    packages=['foobar'],
)
```
