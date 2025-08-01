# Lecture Title

This repo contains the material the lecture material.

It assumes that all software and packages are properly installed and available. Alternatively a Docker container can be build.


## Clone Repository

```         
git clone git@github.com:thomasmanke/website_qmd.git
cd DataScience
```

## Micromamba

The goal is to create an environment (from micromamba.yml + install_packages.sh) within which quarto can be run to produce a web site from qmd files. The same environment can be used to build a web site with github actions (gh-pages).

### Handle environment (create/activate/update/remove)

```         
micromamba env create -n ds -f install/micromamba.yml 
micromamba activate ds

micromamba env update -n ds -f install/micromamba.yml
micromamba remove --name ds --all
```

### Install additional packages

Here are all packages and quarto extensions that could not be installed with conda/micromamba.
Notice that what is conda installable depends on OS version and date.
The goal is to keep install_packages.sh minimal.

```         
micromamba activate ds
./install/install_packages.sh     
```

### Render web site (locally)

```         
#see also: https://github.com/quarto-dev/quarto-cli/discussions/3977
export QUARTO_PYTHON=/Users/manke/miniconda3/envs/ds/bin/python
quarto render
quarto preview
```

### Publish gh-pages (optional)

```         
quarto publish gh-pages
```

Notice that gh-pages will be build with github actions as specified in .github/workflows

## Docker

The Docker container provides a totally isolated Rstudio environment (based on rocker/rstudio) + additional R packages used in this course. The following has been tested

### ... using install2.r

The initial build is very slow but ultimately more reliable. It also required installation of dependencies and libraries before R (apt-get)

```         
cd install
docker build -t ds -f Dockerfile --progress=plain .  &> build.log
docker run -p 8787:8787 --network bridge -e PASSWORD=<my_pwd> -v ${PWD}:/home/rstudio/ds ds
```

### ... using micromamba

This approach would be preferable since

-   it is much faster
-   it parallels the micromamba-based installation above (same micromamba.yml)
-   it is also how things are run as github actions

However this approach was complicated by different host architectures (Linux, Mac OS old vs M2/arm64 --\> uname -a) and could not be solved satisfactory.

```         
cd install
docker build -t ds_mm -f Dockerfile.micromamba . 
docker run -p 8787:8787 --network bridge -e PASSWORD=<my_pwd> -v ${PWD}:/home/rstudio/ds ds_mm
```

Notice:

1.  specifying the platform explicitly in both build and run stage (e.g. with --platform linux/x86_64 ) seemed to work initially, but ultimately the Rstudio would crash after login

2.  I even tried two different ways to integrate micromamba into the rocker/rstudio:

    a\. using a two-stage build process from micromamba image (described here: [mambaorg/micromamba](https://micromamba-docker.readthedocs.io/en/latest/advanced_usage.html) $\to$ Dockerfile.micromamba)

    b\. explicit installation of micromamba (described here: [stackoverflow](https://stackoverflow.com/questions/68193812) -\> Dockerfile.micromamba2)
