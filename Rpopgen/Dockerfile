## Start with the hadleyverse image from Rocker, then add population
## genetics images on top.

FROM rocker/hadleyverse
MAINTAINER Hilmar Lapp hilmar.lapp@duke.edu

## Install population genetics packages from CRAN
RUN rm -rf /tmp/*.rds \
&&  install2.r --error \
    ape \
    adegenet \
    hierfstat \
    pegas \
    mmod \
    genetics

## Install population genetics packages from Github
# (currently there are none)
# RUN installGithub.r

## Install other useful packages from CRAN
RUN rm -rf /tmp/*.rds \
&&  install2.r --error \
    knitcitations \
    phylobase \
    phytools \
&& rm -rf /tmp/downloaded_packages/ /tmp/*.rds

