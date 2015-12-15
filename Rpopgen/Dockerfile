## Start with the hadleyverse image from Rocker, then add population
## genetics images on top.

FROM rocker/hadleyverse
MAINTAINER Hilmar Lapp hilmar.lapp@duke.edu

## Install population genetics packages from CRAN
RUN rm -rf /tmp/*.rds \
&&  install2.r --error \
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
RUN Rscript -e 'source("http://bioconductor.org/biocLite.R"); biocLite("qvalue")'

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

