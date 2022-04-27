# How to install R packges in your personal R library

Because only the login node has access to the internet, it is necessary to do an extra step to install R packages in your personal R library.

You need to be at a command shell on the login node, `172.25.138.10`, also known as `login-10-03` or `compute03`.

If for some reason you are not on `login-10-03`, you can do 

```
module load pbspro
qsub -I -l select=1:ncpus=1:mem=10G:ngpus=0:vnode=computeg03 -l walltime=7200 -q workq
```
(Note that `-l` is minus lower-case L.)

You will then get a shell on the login node.

On the login node, enter the following at the linux shell:

```
module load r
R # Start R
```

To test the setup, we will use a test package, `tinytest`.  

Later, once you have confirmed that you setup is workng, you can replace
tinytest with the packages of your choice.

At the R command prompt, enter

```
install.packages("tinytest", lib = "~/R/rstudio/4.1") 
# 4.1 will change as we move to new R versions
# test that it worked
libary(tinytest)
q()
```

(If you  `qsub`'ed to the login node, exit now.)

Then make sure that the package `tinytest` is also visibible in RStudio
by opening an RStudio session and trying to load it.


If you find problems with the documentation email steverozen@pm.me.
