# How to install R pacakges in your personal R library

Because only the login node has access to the internet, it is necessary to do an extra step to install R packages in your personal R library.

You need to be at a command shell on the login node, `172.25.138.10`.

Enter the following:

```
module load r
R # Start R
```

To test the setup, we will use a test package, `tinytest`

At the R command prompt, enter

```
install.packages("tinytest", lib = "/data/<yourgroup>/home/<your user id>/XXXXXX")
# test that it worked
libary(tinytest)
```

If you find problems with the documentation email steverozen@pm.me.
