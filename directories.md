# Directories in Jupyter Notebook

## CWD

```python
import os

# define directories
cwd = os.getcwd()
```

## Parent Directory

```python
cwd             = os.getcwd()
os.chdir('..')
par_dir         = os.path.abspath(os.curdir)
```

## Parent Directory (multiple levels)

```python
cwd             = os.getcwd()
os.chdir('..')
dir_2017        = os.getcwd()
os.chdir('..')
par_dir         = os.path.abspath(os.curdir)
```
