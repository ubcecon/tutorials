## Install WSL from Ubuntu and Conda

To get "Ubuntu on Windows" and other linux kernels see [instructions](https://docs.microsoft.com/en-us/windows/wsl/install-win10) for installing WSL2.  It is significantly better, but may require you to update your windows version.

Hint on copy-paste:  One way to paste into a Windows terminal (of any sort) is the `<ctrl-c>` text somewhere else and then, while selected in the terminal at the cursor, to `<right click>` the mouse (which pastes)

When wsl is installed, you can go `wsl` in any powershell terminal to enter


## General Setup

To get git credentials integrated, in a windows terminal (i.e. not in the WSL terminal) run
```
 git config --global credential.helper wincred
```
Then in a WSL terminal (within VS Code or otherwise, but replacing with your email and name),
```
git config --global user.email "you@example.com"
git config --global user.name "Your Name"
git config --global credential.helper "/mnt/c/Program\ Files/Git/mingw64/libexec/git-core/git-credential-wincred.exe"
```
(See more details in [Sharing Credentials](https://code.visualstudio.com/docs/remote/troubleshooting#_sharing-git-credentials-between-windows-and-wsl) )

```bash
cd ~
sudo apt update
sudo apt-get upgrade
sudo apt install make gcc unzip
sudo apt-get update
``` 

2. Install Conda

   -  In the Ubuntu terminal, first install python/etc. tools
   ```bash
   wget https://repo.anaconda.com/archive/Anaconda3-2020.07-Linux-x86_64.sh
   bash Anaconda3-2020.07-Linux-x86_64.sh
   ```

## Installing Conda
1. Run `Powershell` as an administrator
2. In the Ubuntu terminal, first install python/etc. tools
```bash
wget https://repo.anaconda.com/archive/Anaconda3-2020.07-Linux-x86_64.sh
bash Anaconda3-2020.07-linux-x86_64.sh
```
   - Create a directory `.conda` by running `mkdir ~/.conda` if the warning "Unable to register the environment" shows up
3. The installation will take time. You should:
   - accept default paths
   - accept licensing terms
   - *IMPORTANT* Manually choose `yes` to have it do the `conda init`
4. (Optional) Delete the installation file
```bash
rm Anaconda3-2020.07-Linux-x86_64.sh
```

## Upgrade Conda
1. Upgrade
```bash
conda upgrade conda
```
2. Install pytorch through conda.  With a GPU:
```bash
conda install pytorch cudatoolkit=11.0 -c pytorch
```
Or without,
```bash
conda install pytorch -c pytorch
```
## More Administration Tips
- You can reset your ubuntu setup by
  - Searching for Ubuntu from the main "Start" icon, right-click on the "Ubuntu" app, Choose "App Settings", then choose "Reset"
