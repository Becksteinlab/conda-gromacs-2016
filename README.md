# README for conda-gromacs-2016

This repository contains everything needed to build
[conda](https://conda.io/docs/) packages for the popular
[Gromacs](http://www.gromacs.org) molecular dynamics package.

**WARNING**: The package builds a **minimal, portable Gromacs version** that is
primarily useful for testing. It is **not recommended to use it for
production-scale simulations.**

Reduced performance features:
* only thread parallelization
* uses bundled FFT (not a fast FFT)
* no GPU support


## Using the installed package

Multiple versions of Gromacs can be installed in parallel. A script
`get_gmx` is installed in the user's home directory that allows the
user to select the desired version of Gromacs. It returns the path to
the `GMXRC` startup script, which in turn needs to be sourced to set
up the Gromacs environment. For instance, to select version
*2016* one would run in the shell

```
source `get_gmx 2016`
```


## Pre-built packages
Anaconda packages for *linux-64* are available in the Anaconda Cloud channel
[anaconda.org/becksteinlab](https://anaconda.org/becksteinlab). If you
have `conda` installed you can install this package with

```
conda install -c becksteinlab gromacs-2016
```

## Building the package
It is recommended to build the package within a minimal docker container. 
Build the docker container by invoking

```
docker build -t gmx_build .
```
in the same directory as the provided Dockerfile.

Start the docker container with `docker run -it gmx_build`. If everything 
works as expected, then you should find yourself in an environment similar
to:

```
[root@0f6a75177395 /]# 
```

Navigate to `/root/gromacs` to find the build scripts. Run: 

```
bash build_conda_package.sh
```

Once this has finished move to the parent directory to find your package in tar.bz2 
archive.

### Keep locally or push to cloud:

#### Copy to host machine
From a new terminal find the container ID with `docker ps`. With this ID, invoke:

```
docker cp <CONTAINER ID>:/root/<CONDA_TAR_BZ2> $OUTPUT_DIR
```

You should be able to find the conda package in the output directory.

To exit the docker container type `exit`.

#### Upload directly to Anaconda cloud

To upload directly to a the Anaconda clound through your Anaconda username, run:
```
anaconda upload -u <ANACONDA USERNAME> <CONDA_TAR_BZ2>
```

To exit the docker container type `exit`

## Licensing

[Gromacs](http://www.gromacs.org/About_Gromacs) itself is published
under the GNU
[Lesser General Public License](http://www.gnu.org/licenses/lgpl-2.1.html)
(LGPL), version 2.1. The files to *build anaconda packages* are
licensed under the MIT license (see file `LICENSE`).


## Contributing

We welcome contributions in the form of issue reports and pull requests.
