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
## GitHubPath

In:
```python
import os
cwd = os.getcwd().replace('\\','/')
print(cwd)
```
Out:
```
C:/Users/<id>/Documents/GitHub/Valuations/Scripts
```

We want just `C:/Users/<id>/Documents/GitHub/`, which we get using this:

In:
```python
import os
cwd = os.getcwd().replace('\\','/')
GitHubPath = cwd[:cwd.find('GitHub/')+len('GitHub/')]
print(GitHubPath)
```

Out:
```
C:/Users/<id>/Documents/GitHub/
```


