# VisualStudio Code Recommendations

The following are heavily opinionated set of suggested packages, tutorials, etc. to use with vscode

## General Packages and Setup

1. Install with [vscode](https://code.visualstudio.com/) and accept defaults if possible
2. (Optional) some highly recommended packages

   - Editing Markdown: https://marketplace.visualstudio.com/items?itemName=yzhang.markdown-all-in-one
   - Extra Git Tools: https://marketplace.visualstudio.com/items?itemName=eamodio.gitlens
   - Spell Checking: https://marketplace.visualstudio.com/items?itemName=streetsidesoftware.code-spell-checker

3. Go to settings with `<Ctrl-Shift-P>` and search for the following settings to change:
   - `files.eol` to `\n`
   - `enablePreviewFromQuickOpen` to turn it off
   - `Tab Size` to `4`

A reminder that it is strongly recommended on Windows to run the following at the commandline

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

## Python

1. First install Python interpreter. Recommendation is https://www.anaconda.com/distribution/
2. Install the main extension: https://marketplace.visualstudio.com/items?itemName=ms-python.python
3. (Optional) Install Code Black Formatter. In console: `pip install black`
   - Go to settings with `<Ctrl-Shift-P>` and change `Python> Formatting Provider` to `black`
4. (Optional) Microsoft Intellicode AI: https://marketplace.visualstudio.com/items?itemName=VisualStudioExptTeam.vscodeintellicode
   - Will need to accept using the preview version of the language server
5. See https://code.visualstudio.com/docs/python/jupyter-support for Jupyter support

If it asks you to choose a python interpretter, choosing `("base": conda)` is fine.

## Julia

1. Install [Julia](https://julialang.org/downloads/) or see https://julia.quantecon.org/getting_started_julia/getting_started.html for more advanced instructions
2. Install the Julia Extension: https://marketplace.visualstudio.com/items?itemName=julialang.language-julia

## Remote Editing, Collaboration, and Other Extensions

- VS LiveShare: https://marketplace.visualstudio.com/items?itemName=MS-vsliveshare.vsliveshare-pack
- Remove SSH editing: https://code.visualstudio.com/docs/remote/ssh
- WSL: https://code.visualstudio.com/docs/remote/wsl
- Jupyter Support (Python only): https://code.visualstudio.com/docs/python/jupyter-support
- Markdown to PDF: https://marketplace.visualstudio.com/items?itemName=yzane.markdown-pdf
- Code Formatter: https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode

  - Downside is it requires the

## Other Tutorials

- https://medium.com/@christyjacob4/using-vscode-remotely-on-an-ec2-instance-7822c4032cff
