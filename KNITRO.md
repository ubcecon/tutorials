# Artelys Knitro

The economics department has a site-license to the [Artelys Knitro](https://www.artelys.com/docs/knitro/) optimization library.

The network license can be used by all faculty and students from the UBC wired or wireless internet, and through the VPN from outside.  Email Jesse for faculty who need an offline license (e.g. to run on airplanes or when the VPN isn't feasible).

This is a commercial optimizer with especially strong support for
- [Nonlinear optimization](https://www.artelys.com/docs/knitro/2_userGuide/minlp.html), including large sparse systems (e.g. into the thousands of variables) and mixed-integrer problems
- [Complementarity constraints](https://www.artelys.com/docs/knitro/2_userGuide/complementarity.html) which come about in many structural estimation and game theoretic models
- [Constrained nonlinear least squares](https://www.artelys.com/docs/knitro/2_userGuide/ktrlsq.html) 
- [Systems of Nonlinear Equations](https://www.artelys.com/docs/knitro/2_userGuide/specialProblems.html#systems-of-nonlinear-equations) either through setting up an objective with equality constraints, or using the nonlinear least squares 
- Lots of options such as [Parallel multi-start](https://www.artelys.com/docs/knitro/2_userGuide/multistart.html#sec-multistart), etc.  which might not 100% work with all languages quite yet.
- The [Tuner](https://www.artelys.com/docs/knitro/2_userGuide/tuner.html) which tries out a bunch of optimization algorithms and reports on the best option for you.

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

For a simple test of the setup, run the following in a new Jupyter notebook 

```julia
using JuMP, KNITRO
m = Model(with_optimizer(KNITRO.Optimizer)) # settings for the solver
@variable(m, x)
@variable(m, y)

@NLobjective(m, Min, (1-x)^2 + 100(y-x^2)^2)

optimize!(m)
println("x = ", value(x), " y = ", value(y))
```


## Useful Features

The JuMP.jl interface is not the only way to access it, but it provides a good baseline to explore features.

You can switch between linear and nonlinear with the `@objective` vs. `@NLobjective` or `@constraint` vs. `@NLconstraint`.

For example, using a linear objective and nonlinear constraints

```julia 
using JuMP, KNITRO
# solve
# max( x[1] + x[2] )
# st sqrt(x[1]^2 + x[2]^2) <= 1

m = Model(with_optimizer(KNITRO.Optimizer))

@variable(m, x[1:2])
@objective(m, Max, sum(x))
@NLconstraint(m, sqrt(x[1]^2+x[2]^2) <= 1)
@show optimize!(m)
```

- Note that `x` is defined as a vector of length `2`
- Also, note that the Knitro is providing a bunch of output on the identification of the problem, and the choice of algorithms
  - e.g. `algorithm from AUTO to 1`, and `bar_murule from AUTO to 4`
  - This is the result of heuristics that Knitro is using to figure out the best options for the algorithm choice.  You can manually change these settings, as well as use the tuner to explore variations on them.


The following code snippet is the same example as above, but using more of KNITRO's functionality. 

```julia
using JuMP, KNITRO
# m = Model(with_optimizer(KNITRO.Optimizer, ms_enable = 1, honorbnds = 1, outlev = 1, algorithm = 4)) # (1)
m = Model(with_optimizer(KNITRO.Optimizer, honorbnds = 1, outlev = 1, algorithm = 4)) # (1)
@variable(m, x, start = 1.2) #(5)
@variable(m, y)
@variable(m, z)
@variable(m, v)
@variable(m, 4.0 <= u <= 4.0) # (2)

mysquare(x) = x^2 
register(m, :mysquare, 1, mysquare, autodiff = true) # (3)

@NLobjective(m, Min, mysquare(1 - x) + 100(y-x^2)^2 + u) 
@constraint(m, z == x + y)
@constraint(m, v == 5.0) # (4)

optimize!(m)
(value(x), value(y), value(z), value(v), value(u), objective_value(m), termination_status(m)) # (5)
```

- (1), we see a few options: 

  * `ms_enable = 1`, which turns on multistart. This starts the solver from a few different initial conditions, and takes the minimum over all runs.  This may require `KNITRO#master` if it fails.

  * `outlev = 1`. A little printing. Other options are `outlev = 0, 1, 2, 3, 4, 5, 6`. See [here](https://www.artelys.com/docs/knitro/3_referenceManual/userOptions.html#outlev) for what each does. 

  * `honorbnds = 1`. Forces intermediate iterates to satisfy the box bounds (not just the initial point and solution). Helps if the bounds define a feasible space, outside of which the problem is ill-behaved. Note that this does not apply to the nonlinear constraints, and probably doesn't apply to linear constraints.

  * `algorithm = 4` chooses the SQP algorithm instead of letting Knitro determine the auto choice. See [here](https://www.artelys.com/docs/knitro//2_userGuide/algorithms.html) for algorithm choices.


- (2) initial condition for a variable
- (3) and (4) A lower box-bound on the `v` value, where the upper bound is assumed to be infinite, and a two-sided box bound on `u`.
- (5) we register our own function `mysquare` for auto-differentiation for use in the model.
  - Otherwise, the `@NLobjective` and `@NLconstraint` can only handle some basic built-in functions such as powers, sum, etc.
  - The arguments are: `(model, :name_in_the_model, number_of_arguments, name_in_julia, autodiff = true)`
  - If you have parameters you don't want to pass to the solver, create a closure (e.g. `f_fixed(x) = f(x, p)`, where `p` is a bunch of parameters, and then register `f_fixed` instead.
- (6) provide a linear constraint.  Note that we use `@constraint` and not `@NLconstraint`.
- (7) A linear equality constraint that `u` that is fixed at 4.
   - If you look at the output, it says `Knitro presolve eliminated 1 variable and 1 constraint`
   - This means that Knitro figured out that the variable didn't need to be solved for, and eliminated the constraint and variable
   - While this is trivial to see here, sometimes this can help dramatically when the fixed constraints and values are less obvious
   - A lesson is that you shoouldn't worry about putting on lots of linear constraints.
- (8) Access  results from the optimized model. For more on the outputs and getter functions, see [here](http://www.juliaopt.org/JuMP.jl/v0.19.0/solutions/).

For the full list of KNITRO solver options, see [here](https://www.artelys.com/docs/knitro/3_referenceManual/userOptions.html).

## Tuner
As with most solvers, there are a number of variations on the parameters and algorithms, which can have differences in the speed of convergence.  It won't matter for a problem this small and simple, but for real problems it can be dramatic.

The `tuner = 1` option enables the KNITRO [solver parameter tuner](https://www.artelys.com/docs/knitro//2_userGuide/tuner.html#sec-tuner) which will try out various algorithm and setting shoices.  You generally would only run this once and then use the best options in the `algorithm` etc. later.

```julia
using JuMP, KNITRO
m = Model(with_optimizer(KNITRO.Optimizer, tuner = 1)) # (1)
@variable(m, x, start = 1.2) #(2)
@variable(m, y)
@variable(m, z)
@variable(m, v >= 0.0) # (3)
@variable(m, -4.0 <= u <= 4.0) # (4)

mysquare(x) = x^2 
register(m, :mysquare, 1, mysquare, autodiff = true) # (5)

@NLobjective(m, Min, mysquare(1 - x) + 100(y-x^2)^2 + u) 
@constraint(m, z == x + y) # (6)
@constraint(m, v == 5.0) # (7)

optimize!(m)
```
The output says that `Knitro Tuner will explore up to 48 option combinations` and then goes through a number of permutations.
At the edn, it may give output such as 
```
Tuner non-default option settings for this solve are:
algorithm:            1
bar_murule:           5
hessopt:              1
hessian_no_f:         1
linsolver:            4
```
Which tells you which options you could set to get the fastest execution time.  (e.g. `m = Model(with_optimizer(KNITRO.Optimizer, algorithm = 1, bar_murule=5)` etc.)

However, unless the differences are dramatic, you may be better off leaving the default options.


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
