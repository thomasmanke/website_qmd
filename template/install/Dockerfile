# rocker/rstudio is Ubuntu - see: docker run --rm rocker/rstudio cat /etc/os-release 
# Notice that rocker/rstudio:4.3+ is based on ubuntu 22.04 which may have issues with apt-get update
FROM rocker/rstudio:latest
#FROM rocker/rstudio:4.2.0

# needed for magick and tidyverse    
RUN apt-get update && apt-get install -y libmagick++-dev libharfbuzz-dev libfribidi-dev 

#RUN apt-get install -y libmagick++-dev libharfbuzz-dev libfribidi-dev

# install additional R packages
RUN install2.r tidyverse patchwork pheatmap \ 
    DBI duckdb bigrquery magick && \
    rm -rf /tmp/downloaded_packages

RUN install2.r codetools brms gapminder
RUN install2.r caret keras

# RUN mamba install -y --file micromamba.yml
#RUN /rocker_scripts/install_shiny_server.sh
