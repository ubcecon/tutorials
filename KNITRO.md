# Artelys Knitro

The economics department has a site-license to the [Artelys Knitro](https://www.artelys.com/docs/knitro/) optimization library.

The network license can be used by all faculty and students from the UBC wired or wireless internet, and through the VPN from outside.  Email Jesse for faculty who need an offline license (e.g. to run on airplanes or when the VPN isn't feasible).

This is a commercial optimizer with especially strong support for
- [Nonlinear optimization](https://www.artelys.com/docs/knitro/2_userGuide/minlp.html), including large sparse systems (e.g. into the thousands of variables) and mixed-integrer problems
- [Complementarity constraints](https://www.artelys.com/docs/knitro/2_userGuide/complementarity.html) which come about in many structural estimation and game theoretic models
- [Constrained nonlinear least squares](https://www.artelys.com/docs/knitro/2_userGuide/ktrlsq.html) 
- [Systems of Nonlinear Equations](https://www.artelys.com/docs/knitro/2_userGuide/specialProblems.html#systems-of-nonlinear-equations) either through setting up an objective with equality constraints, or using the nonlinear least squares 
- Lots of options such as [Parallel multi-start](https://www.artelys.com/docs/knitro/2_userGuide/multistart.html#sec-multistart), etc.   There is a [Tuner](https://www.artelys.com/docs/knitro/2_userGuide/tuner.html) which may also be useful.

## Programming languages

The Knitro license is avaiable for use within Julia, Matlab, Python, C/C++, and even Fortran.  See the documentation for different languages.


## General Setup

To use our network license, first download the binaries

- [OS/X](https://s3-us-west-2.amazonaws.com/jesseperla.com/knitro/knitro-12.0.0-z-MacOS-64.tar.gz)
- [Linux](https://s3-us-west-2.amazonaws.com/jesseperla.com/knitro/knitro-12.0.0-z-Linux-64.tar.gz)

### JupyterHub (vse.syzygy.ca)

It is preinstalled.  With Julia, just go `using KNITRO`.

### Windows
1. [Download the installer](https://s3-us-west-2.amazonaws.com/jesseperla.com/knitro/Knitro1200Installer_64.exe)
2. Click on the installer and execute it (ignoring security warnings).  When it asks for a license file, hit next to avoid choosing one
3. After the installation is complete, open up a powershell or cmd terminal and run the following:
```
setx ARTELYS_LICENSE_NETWORK_ADDR "137.82.185.3:8349"
```
4. Installing the front-end libraries then depends on the particular programming languages.  For Julia, just open a julia terminal and go
```
] add KNITRO
```

### OSX
0. Navigate in a terminal to where you would want to install the software
1. Download the binary from [here](https://s3-us-west-2.amazonaws.com/jesseperla.com/knitro/knitro-12.0.0-z-MacOS-64.tar.gz) and unpack, or just execute
```
wget -qO- https://s3-us-west-2.amazonaws.com/jesseperla.com/knitro/knitro-12.0.0-z-MacOS-64.tar.gz | tar -xzv
```
2. TBD: How/where to change the environment varaibles.  ARNAV?  Can this be more idiot proof so modifying the path isn't needed?  Expand instructions
```
export ARTELYS_LICENSE_NETWORK_ADDR="137.82.185.3:8349"
export DYLD_LIBRARY_PATH="/Users/USERNAME/knitro-12.0.0-z-MacOS-64/lib"
export KNITRODIR="/Users/USERNAME/knitro-12.0.0-z-MacOS-64"
```
3. Then `] add KNITRO` in Julia.

### Linux
0. Navigate in a terminal to where you would want to install the software
1. Download the binary from [here](https://s3-us-west-2.amazonaws.com/jesseperla.com/knitro/knitro-12.0.0-z-Linux-64.tar.gz) and unpack, or just execute
```
wget -qO- https://s3-us-west-2.amazonaws.com/jesseperla.com/knitro/knitro-12.0.0-z-Linux-64.tar.gz | tar -xzv
```
2. TBD: How/where to change the environment varaibles.  ARNAV?  Can this be more idiot proof so modifying the path isn't needed?  Expand instructions
```
export ARTELYS_LICENSE_NETWORK_ADDR="137.82.185.3:8349"
export DYLD_LIBRARY_PATH="/Users/USERNAME/knitro-12.0.0-z-MacOS-64/lib"
export KNITRODIR="/Users/USERNAME/knitro-12.0.0-z-MacOS-64"
```
3. Then `] add KNITRO` in Julia.


## Hints

- Knitro will make some decisions on its own, but experimenting with the [different algorithms](https://www.artelys.com/docs/knitro/2_userGuide/algorithms.html) is generally a good idea for problems where performance matters.
