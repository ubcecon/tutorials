# Python Links and Tutorials

## Project/Repo Structure
It is worth your effort to standardize on repository structures to make analysis/collaboration/reproducibility easier.
- See https://drivendata.github.io/cookiecutter-data-science/  for a datascience oriented structure.  It doesn't always apply for every economics project, but follow it if you can
- A bigger framework for setting up solid ML/datascience pipelines is https://kedro.readthedocs.io/en/stable/ 
- Do not invent your own structure! 

## Interactive Work with Python Files
For displaying graphs/output/etc. inline, create a file
```python
import matplotlib.pyplot as plt
import numpy as np
x = np.linspace(0, 20, 100)  # Create a list of evenly-spaced numbers over the range
plt.plot(x, np.sin(x))       # Plot the sine of each x point
plt.show()     
```
And then `<Ctrl-Shift-P>` to enter the command, and choose `> Run Current File in Python Python Interactive window`  to see plots in the interactive terminal.

Alternatively, you can run the file directly in normal terminal
 - You may see the error `qt.qpa.plugin: Could not load the Qt platform plugin "windows" in "" even though it was found.`
 - If so, then there may be changes required.  Possible miktex collision setting the `QT_PLUGIN_PATH`? See https://stackoverflow.com/questions/41994485/error-could-not-find-or-load-the-qt-platform-plugin-windows-while-using-matplo  



## VSCode Tricks

- When  `code black` is installed as the default in vscode, `<Ctrl-Shift-P>` to find `Format` or choose `Shift-Alt-F` to format with the standard 
- `<Shift-Enter>` in a `.py` file will run the python in an interactive window or terminal

## PyTorch
- Extension: https://marketplace.visualstudio.com/items?itemName=SBSnippets.pytorch-snippets
- Tutorials
  - https://pytorch-for-numpy-users.wkentaro.com/