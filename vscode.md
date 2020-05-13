# VisualStudio Code Recommendations

The following are heavily opinionated set of suggested packages, tutorials, etc. to use with vscode

## General Packages and Setup

1. Install with [vscode](https://code.visualstudio.com/) and accept defaults if possible
   - After installation of vscode, you should be able to click `Install` link on the webpage of any extensions
2. (Optional) some highly recommended packages

   - Github Support: https://marketplace.visualstudio.com/items?itemName=GitHub.GitHubExtensionforVisualStudio
   - Editing Markdown: https://marketplace.visualstudio.com/items?itemName=yzhang.markdown-all-in-one
   - Extra Git Tools: https://marketplace.visualstudio.com/items?itemName=eamodio.gitlens
   - Spell Checking: https://marketplace.visualstudio.com/items?itemName=streetsidesoftware.code-spell-checker
   - Markdown to PDF: https://marketplace.visualstudio.com/items?itemName=yzane.markdown-pdf
   - Code Formatter: https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode
   - YAML support: https://marketplace.visualstudio.com/items?itemName=redhat.vscode-yaml

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

1. Setup latex with either TeXLive or MikTeX (on Windows)
   - In order for SyncTex to work properly on MikTex  you may need to update to a more recent version using the miktex console
   
2. Install the extension:
   https://marketplace.visualstudio.com/items?itemName=James-Yu.latex-workshop
3. Install spellchecker:
   https://marketplace.visualstudio.com/items?itemName=streetsidesoftware.code-spell-checker

The easiest way to compile is to put magic comments at the top of documents (consistent across many editors). For example,

```latex
% !TEX program = pdflatex
% !BIB program = bibtex
% !TEX enableSynctex = true
```
or for a more modern latex compilation, you could try `% !TEX program = lualatex` or `% !TEX program = xelatex`

## Julia

1. Install [Julia](https://julialang.org/downloads/) or see https://julia.quantecon.org/getting_started_julia/getting_started.html for more advanced instructions
2. Install the Julia Extension: https://marketplace.visualstudio.com/items?itemName=julialang.language-julia
3. (Optional) TOML: https://marketplace.visualstudio.com/items?itemName=bungcip.better-toml

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

- Core Remote Extensions:
  - Install OpenSSH client if required:
    - https://docs.microsoft.com/en-us/windows-server/administration/openssh/openssh_install_firstuse
  - Remote Extensions: https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.vscode-remote-extensionpack
- SFTP Support: https://marketplace.visualstudio.com/iems?itemName=liximomo.sftp 
- VS LiveShare: https://marketplace.visualstudio.com/items?itemName=MS-vsliveshare.vsliveshare-pack

## Other Tutorials
-  Remote Development Docs:
    - General: https://code.visualstudio.com/docs/remote/remote-overview 
    - Remove SSH editing: https://code.visualstudio.com/docs/remote/ssh
    - WSL: https://code.visualstudio.com/docs/remote/wsl
- https://medium.com/@christyjacob4/using-vscode-remotely-on-an-ec2-instance-7822c4032cff
