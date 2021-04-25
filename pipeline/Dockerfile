FROM amazonlinux:latest

LABEL version="1.0" maintainer="Firas Sadiyah <Firas [dot] Sadiyah [at] GMail>"

COPY environment.yml /

RUN  yum -y update && \
    # update the system and install dependencies
    yum -y install bzip2 unzip zip wget procps vim && \
    # download latest miniconda script
    wget https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh && \
    # install miniconda
    bash Miniconda3-latest-Linux-x86_64.sh -b -f -p -b -p /opt/conda && \
    # updated conda
    /opt/conda/bin/conda update -y conda && \
    # install packages
    /opt/conda/bin/conda env create -f /environment.yml && \
    # clean conda
    /opt/conda/bin/conda clean -afy && \
    # export a list of installed packages with their versions
    /opt/conda/bin/conda env export --name pipeline > pipeline.yml && \
    # remove miniconda installer script
    rm Miniconda3-latest-Linux-x86_64.sh

# add conda environment bin to the PATH
ENV PATH /opt/conda/envs/pipeline/bin:$PATH
