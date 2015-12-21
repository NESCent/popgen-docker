## Start with the hadleyverse image from Rocker, then add population
## genetics images on top.

FROM rocker/hadleyverse
MAINTAINER Hilmar Lapp hilmar.lapp@duke.edu

## OpenBLAS is having some issues at the moment, this installs Atlas BLAS
RUN apt-get update \
&&  apt-get remove -y libopenblas-base \
&&  apt-get install -y libatlas-base-dev

## Bioconductor dependencies of packages we install from CRAN (specifically pegas)
RUN Rscript -e 'source("http://bioconductor.org/biocLite.R"); biocLite("Biostrings");'

## Install population genetics packages from CRAN
RUN rm -rf /tmp/*.rds \
&&  install2.r --error \
    apex \
    ape \
    adegenet \
    pegas \
    coalescentMCMC \
    mmod \
    poppr \
    strataG \
    rmetasim \
    genetics \
    hierfstat \
&& rm -rf /tmp/downloaded_packages/ /tmp/*.rds

## Bioconductor packages (they may be dependencies)
RUN Rscript -e 'source("http://bioconductor.org/biocLite.R"); biocLite("qvalue");'

## Install population genetics packages from Github
## (hierfstat included here temporarily until new release is on CRAN)
RUN installGithub.r \
    whitlock/OutFLANK \
&& rm -rf /tmp/downloaded_packages/ /tmp/*.rds

## Install other useful packages from CRAN
RUN install2.r --error \
    knitcitations \
    phangorn \
    phylobase \
    phytools \
&& rm -rf /tmp/downloaded_packages/ /tmp/*.rds

