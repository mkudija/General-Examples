# mplstlye

The Matplotlib sytle file allows you to stylize plots. 
- The `mag` style uses standard GE colors, font, etc.
- The `Root` style uses standard [Root](https://www.joinroot.com/guide/color) colors, font, etc.

Drop the `root.mplstyle` file into the appropriate directory:
- Mac: `/Users/matthewkudija/.matplotlib/stylelib/`
- Windows: `C:\Users\212574846\AppData\Local\Continuum\Anaconda3\Lib\site-packages\matplotlib\mpl-data\stylelib`

If you cannot find the directory, run this command:
```python
import matplotlib
matplotlib.get_configdir()
```

Then call the style using:

`plt.style.use('root')`
