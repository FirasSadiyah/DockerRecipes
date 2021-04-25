# Docker image for Ubuntu 20.04, R 4, RStudio Server 1.2.5042
LABEL version="1.0" maintainer="Firas Sadiyah <Firas [dot] Sadiyah [at] GMail>"

# Adapted from https://github.com/rocker-org/rocker-versioned2/blob/master/dockerfiles/Dockerfile_r-ver_devel
# Adapted from https://gist.github.com/snystrom/eca67d993c579c3416cda63590d9080a

FROM rocker/r-ver:devel

ENV S6_VERSION=v1.21.7.0

ENV RSTUDIO_VERSION=latest
ENV PATH=/usr/lib/rstudio-server/bin:$PATH

RUN /rocker_scripts/install_rstudio.sh
RUN /rocker_scripts/install_pandoc.sh
RUN /rocker_scripts/install_tidyverse.sh


RUN apt-get update && apt-get install -y \
  htop \
  libbz2-dev \
  libcairo2-dev \
  libcurl4-openssl-dev \
  libfreetype6-dev \
  libfribidi-dev \
  libgsl-dev \
  libharfbuzz-dev \
  libjpeg-dev \
  liblzma-dev \
  libnode-dev\
  libpixman-1-dev \
  libpng-dev \
  libproj-dev \
  librsvg2-dev \
  libtiff5-dev \
  libv8-dev\
  libx11-dev \
  libxt-dev \
  libz-dev \
  tmux \
  zlib1g-dev \
  && rm -rf /var/lib/apt/lists/*

RUN Rscript -e "install.packages('BiocManager')"
RUN Rscript -e "install.packages('devtools')"
RUN Rscript -e "install.packages('ggrastr')"
RUN Rscript -e "BiocManager::install('DiffBind')"
RUN Rscript -e "BiocManager::install('qrqc')"

EXPOSE 8787

CMD ["/init"]
