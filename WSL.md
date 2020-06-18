## Install WSL from Ubuntu and Conda

To get "Ubuntu on Windows" and other linux kernels see [instructions](https://docs.microsoft.com/en-us/windows/wsl/install-win10) for installing WSL2.  It is significantly better, but may require you to update your windows version.

Hint on copy-paste:  One way to paste into a Windows terminal (of any sort) is the `<ctrl-c>` text somewhere else and then, while selected in the terminal at the cursor, to `<right click>` the mouse (which pastes)

## Installing Conda
1. Run `Powershell` as an administrator
2. In the Ubuntu terminal, first install python/etc. tools
```bash
wget https://repo.anaconda.com/archive/Anaconda3-2020.02-Linux-x86_64.sh
bash Anaconda3-2020.02-Linux-x86_64.sh
```
   - Create a directory `.conda` by running `mkdir ~/.conda` if the warning "Unable to register the environment" shows up
3. The installation will take time. You should:
   - accept default paths
   - accept licensing terms
   - *IMPORTANT* Manually choose `yes` to have it do the `conda init`
4. (Optional) Delete the installation file
```bash
rm Anaconda3-2020.02-Linux-x86_64.sh
```

## More Administration Tips
- You can reset your ubuntu setup by
  - Searching for Ubuntu from the main "Start" icon, right-click on the "Ubuntu" app, Choose "App Settings", then choose "Reset"
