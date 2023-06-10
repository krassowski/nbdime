# Contributing

We follow the [IPython Contributing Guide](https://github.com/ipython/ipython/blob/master/CONTRIBUTING.md).

## JupyterLab extension

To install the JupyterLab frontend extension in development mode, instead of <s>`jupyter labextension develop . --overwrite`</s>,
run the following Python script from the top-level directory of this repository:

```python
from jupyterlab.federated_labextensions import develop_labextension
from jupyterlab.labapp import LabApp

lab = LabApp()
lab.load_config_file()
develop_labextension(
    'nbdime/labextension',
    labextensions_dir=lab.labextensions_path[0],
    destination='nbdime-jupyterlab',
    overwrite=True,
    symlink=True   # for Windows see documentation on enabling symlinks first
)
```

Then to update, manually recompile by running:

```
jlpm build
```

If your system supports `inotify`, you can auto-recompile on changes with:

```
while inotifywait -e close_write *; do jlpm build; done
```
