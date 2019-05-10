## Start with the hadleyverse image from Rocker, then add population
## genetics images on top.

FROM rocker/tidyverse:latest
MAINTAINER Hilmar Lapp hilmar.lapp@duke.edu

# Prevent error messages from debconf about non-interactive frontend
ARG TERM=linux
ARG DEBIAN_FRONTEND=noninteractive

## Some of the R packages depend on libraries not already installed in the
## base image, so they need to be installed here for the R package
## installations to succeed.
RUN apt-get update \
    && apt-get install -y \
    libgsl0-dev \
    libmagick++-dev \
    libudunits2-dev \
    gdal-bin \
    libgdal-dev

## The nloptr package is needed by lme4, and it itself needs to download the
## NLopt code from http://ab-initio.mit.edu/wiki/index.php/NLopt, which is
## unstable. Hence we put this upfront, so that we fail fast on this step,
## which makes it easier to redo.
RUN install2.r --error \
    nloptr \
&& rm -rf /tmp/downloaded_packages/ /tmp/*.rds

## Bioconductor dependencies of packages we install from CRAN (specifically pegas)
RUN install2.r --error BiocManager \
&& Rscript -e 'requireNamespace("BiocManager"); BiocManager::install();' \
&& Rscript -e 'requireNamespace("BiocManager"); BiocManager::install(c("Biostrings", "qvalue"));' \
&& rm -rf /tmp/downloaded_packages/ /tmp/*.rds

## Install population genetics packages from CRAN
RUN rm -rf /tmp/*.rds \
&&  install2.r --error \
    apex \
    ape \
    adegenet \
    adespatial \
    pegas \
    phangorn \
    phylobase \
    coalescentMCMC \
    mmod \
    poppr \
    psych \
    strataG \
    rmetasim \
    genetics \
    hierfstat \
    lme4 \
    MuMIn \
    multcomp \
    raster \
    vegan \
    viridis \
    pcadapt \
&& rm -rf /tmp/downloaded_packages/ /tmp/*.rds

## Install population genetics packages from Github
## (hierfstat included here temporarily until new release is on CRAN)
RUN installGithub.r \
    whitlock/OutFLANK \
&& rm -rf /tmp/downloaded_packages/ /tmp/*.rds

## Install other useful packages from CRAN
RUN install2.r --error \
    knitcitations \
    phytools \
&& rm -rf /tmp/downloaded_packages/ /tmp/*.rds

