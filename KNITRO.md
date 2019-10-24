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

2. Open your `~/.bash_profile` file (if it doesn't exist, run `cd` and then `touch .bash_profile` to create it.) Inside, add:  

```
export KNITRODIR="~/path/to/knitro/directory"
export DYLD_LIBRARY_PATH="$KNITRODIR/lib"
export ARTELYS_LICENSE_NETWORK_ADDR="turtle.econ.ubc.ca:8349"
```

**Note:** If you already have something in `DYLD_LIBRARY_PATH`, you will need to append this folder; e.g., `export DYLD_LIBRARY_PATH="$KNITRODIR/lib:$DYLD_LIBRARY_PATH`. But most likely that variable will be empty. 

3. Then `] add KNITRO` in Julia.


### Linux

0. Navigate in a terminal to where you would want to install the software

1. Download the binary from [here](https://s3-us-west-2.amazonaws.com/jesseperla.com/knitro/knitro-12.0.0-z-Linux-64.tar.gz) and unpack, or just execute

```
wget -qO- https://s3-us-west-2.amazonaws.com/jesseperla.com/knitro/knitro-12.0.0-z-Linux-64.tar.gz | tar -xzv
```

2. Open your `~/.bash_profile` file (if it doesn't exist, run `cd` and then `touch .bash_profile` to create it.) Inside, add:  

```
export KNITRODIR="~/path/to/knitro/directory"
export ARTELYS_LICENSE_NETWORK_ADDR="turtle.econ.ubc.ca:8349"
export LD_LIBRARY_PATH="$KNITRODIR/lib"
```

**Note:** If you already have something in `LD_LIBRARY_PATH`, you will need to append this folder; e.g., `export LD_LIBRARY_PATH="$KNITRODIR/lib:$LD_LIBRARY_PATH"`. But most likely that variable will be empty. 

3. Then `] add KNITRO` in Julia.


## Setup Test

For a discrete test of the setup, run the following in a new Jupyter notebook 

```julia
using JuMP,KNITRO
m = Model(with_optimizer(KNITRO.Optimizer)) # settings for the solver
@variable(m, x, start = 0.0)
@variable(m, y, start = 0.0)

@NLobjective(m, Min, (1-x)^2 + 100(y-x^2)^2)

JuMP.optimize!(m)
println("x = ", value(x), " y = ", value(y))
```

We can also do one for a nonlinear objective 

```julia 
using JuMP, KNITRO
# solve
# max( x[1] + x[2] )
# st sqrt(x[1]^2 + x[2]^2) <= 1

m = Model(with_optimizer(KNITRO.Optimizer))

@variable(m, x[1:2], start=0.5) # start is the initial condition
@objective(m, Max, sum(x))
@NLconstraint(m, sqrt(x[1]^2+x[2]^2) <= 1)
@show JuMP.optimize!(m)
```

## Useful Features 

The following code snippet is the same example as above, but using more of KNITRO's functionality. 

```
using JuMP, KNITRO
m = Model(with_optimizer(KNITRO.Optimizer, ms_enable = 1, honorbnds = 1, outlev = 0)) # (1)
@variable(m, x, start = 0.0)
@variable(m, y, start = 0.0)
@variable(m, z, start = 0.0)
@variable(m, v, start = 0.0)
@variable(m, 4.0 <= u <= 4.0) # (2)

@NLobjective(m, Min, (1-x)^2 + 100(y-x^2)^2)
@constraint(m, z == x + y)
@constraint(m, v == 5.0) # (3)

JuMP.optimize!(m)
(value(x), value(y), value(z), value(v), value(u), objective_value(m), termination_status(model)) # (4)
```

In line (1), we set three options: 

* `ms_enable = 1`, which turns on multistart. This starts the solver from a few different initial conditions, and takes the minimum over all runs.

* `outlev = 0`. Minimum amount of printing. Other options are `outlev = 1, 2, 3, 4, 5, 6`. See [here](https://www.artelys.com/docs/knitro/3_referenceManual/userOptions.html#outlev) for what each does. 

* `honorbnds = 1`. Forces intermediate iterates to satisfy the bounds (not just the initial point and solution.) Helps if the bounds define a feasible space, outside of which the problem is ill-behaved. 

In line (2), we define a variable `u` that is fixed at 4 through box bounds. 

In line (3), we fix `v` at 5.0 in a different way (through a constraint.) Note that the initial condition for `v` is 0.0, after which it will "snap" to 5.0

Line (4) is how we query results from the optimized model. For more on the outputs and getter functions, see [here](http://www.juliaopt.org/JuMP.jl/v0.19.0/solutions/).

For the full list of KNITRO solver options, see [here](https://www.artelys.com/docs/knitro/3_referenceManual/userOptions.html).

**Note:** If you see an error like `AttributeNotSupported`, this is likely because the `JuMP` interface for KNITRO has a bug. If that feature is essential, consider using the KNITRO-specific API found [here](https://www.artelys.com/docs/knitro/3_referenceManual/knitroJuliareference.html).

## Hints

- Knitro will make some decisions on its own, but experimenting with the [different algorithms](https://www.artelys.com/docs/knitro/2_userGuide/algorithms.html) is generally a good idea for problems where performance matters.

- If your box bound is not a numeric literal (i.e., `x >= k` for some constant `k`), then `x` always needs to be on the left. That is: 

```julia 
@variable(m, x >= k) # OK 
```

```julia 
@variable(m, k <= x) # not OK 
```