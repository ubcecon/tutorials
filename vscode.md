# VisualStudio Code Recommendations

The following are heavily opinionated set of suggested packages, tutorials, etc. to use with vscode

## General Packages and Setup

1. Install with [vscode](https://code.visualstudio.com/) and accept defaults if possible
   - After installation of vscode, you should be able to click `Install` link on the webpage of any extensions
2. (Optional) some highly recommended packages

   - Editing Markdown: https://marketplace.visualstudio.com/items?itemName=yzhang.markdown-all-in-one
   - Extra Git Tools: https://marketplace.visualstudio.com/items?itemName=eamodio.gitlens
   - Spell Checking: https://marketplace.visualstudio.com/items?itemName=streetsidesoftware.code-spell-checker
   - Markdown to PDF: https://marketplace.visualstudio.com/items?itemName=yzane.markdown-pdf
   - Code Formatter: https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode

3. Go to settings with `<Ctrl-Shift-P>` and search for the following settings to change:
   - `files.eol` to `\n`
   - `enablePreviewFromQuickOpen` to turn it off
   - `Tab Size` to `4`

A reminder that it is strongly recommended on Windows to run the following at the command-line (assuming you installed )

```bash
git config --global core.eol lf
git config --global core.autocrlf false
```

## Latex

1. Setup latex with either TeXLive or MikTeX (on windows)
2. If you are on miktex on windows, manually install SyncTex
   - Recommended approach:
     - Install [Chocaletey](https://chocolatey.org/install), a generally useful windows package manager
     - Right click on Cmd or Powershell to run as administrator, and then simply type `choco install synctex`
   - Alternatively, file files and install manually
     - Download [synctex.exe](https://www.tug.org/svn/texlive/trunk/Master/bin/win32/synctex.exe?revision=53994&view=co)
     - Download [kpathsea632.dll](https://www.tug.org/svn/texlive/trunk/Master/bin/win32/kpathsea632.dll?revision=53994&view=co)
     - Put both files in your mitex binaries folder. Usually something like `C:\Program Files\MiKTeX 2.9\miktex\bin\x64 or C:\Users\USERNAME\AppData\Local\Programs\MiKTeX 2.9\miktex\bin\x64`
3. Install the extension:
   https://marketplace.visualstudio.com/items?itemName=James-Yu.latex-workshop
4. Install spellchecker:
   https://marketplace.visualstudio.com/items?itemName=streetsidesoftware.code-spell-checker

The easiest way to compile is to put magic comments at the top of documents (consistent across many editors). For example,

```latex
% !TEX program = pdflatex
% !BIB program = bibtex
% !TEX enableSynctex = true
```

## Julia

1. Install [Julia](https://julialang.org/downloads/) or see https://julia.quantecon.org/getting_started_julia/getting_started.html for more advanced instructions
2. Install the Julia Extension: https://marketplace.visualstudio.com/items?itemName=julialang.language-julia

## Python

1. First install Python interpreter. Recommendation is https://www.anaconda.com/distribution/
2. Install the main extension: https://marketplace.visualstudio.com/items?itemName=ms-python.python
3. (Optional, but Recommended) Extensions
   1. Code Black Formatter. In console: `pip install black`
      - Go to settings with `<Ctrl-Shift-P>` and change `Python> Formatting Provider` to `black`
   2. Microsoft Intellicode AI: https://marketplace.visualstudio.com/items?itemName=VisualStudioExptTeam.vscodeintellicode
      - Will need to accept using the preview version of the language server
   3. Generating Consistent Docstrings: https://marketplace.visualstudio.com/items?itemName=njpwerner.autodocstring
4. See https://code.visualstudio.com/docs/python/jupyter-support for Jupyter support
   - If you installed `conda` for your python setup, things should work immediately. 

Note: If it asks you to choose a python environment, choosing `("base": conda)` is fine as the default.

## Remote Editing, Collaboration, and Other Extensions

- VS LiveShare: https://marketplace.visualstudio.com/items?itemName=MS-vsliveshare.vsliveshare-pack
- Remove SSH editing: https://code.visualstudio.com/docs/remote/ssh
- WSL: https://code.visualstudio.com/docs/remote/wsl

## Other Tutorials

- https://medium.com/@christyjacob4/using-vscode-remotely-on-an-ec2-instance-7822c4032cff
