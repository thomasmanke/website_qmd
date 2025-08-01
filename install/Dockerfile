# This example Dockerfile is used to create a Docker image for RStudio with additional R packages installed.
# rocker/rstudio is Ubuntu - see: docker run --rm rocker/rstudio cat /etc/os-release 
FROM rocker/rstudio:latest

# needed for magick and tidyverse    
RUN apt-get update && apt-get install -y libmagick++-dev libharfbuzz-dev libfribidi-dev 

# install additional R packages as needed
RUN install2.r tidyverse patchwork pheatmap \ 
    DBI duckdb bigrquery magick && \
    rm -rf /tmp/downloaded_packages

RUN install2.r codetools brms gapminder
RUN install2.r caret keras

# RUN mamba install -y --file micromamba.yml
