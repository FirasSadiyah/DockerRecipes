FROM ubuntu:20.04
LABEL version="1.0" maintainer="Firas Sadiyah <Firas [dot] Sadiyah [at] GMail>"

# Set the time zone
ENV TZ=Europe/London
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

# Set the environment
ENV LANG=C.UTF-8 LC_ALL=C.UTF-8
ENV PATH=/opt/conda/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin

# Update the system
RUN apt-get update --fix-missing \
    &&     apt-get install -y \
           build-essential \
           wget \
           tar \
           curl \
           libtool \
           bzip2 libz-dev ca-certificates libglib2.0-0 libxext6 libsm6 libxrender1 git mercurial subversion \
    &&     apt-get clean

# Install miniconda
RUN wget --quiet https://repo.anaconda.com/miniconda/Miniconda2-4.7.10-Linux-x86_64.sh -O ~/miniconda.sh \
    &&     /bin/bash ~/miniconda.sh -b -p /opt/conda \
    &&     rm ~/miniconda.sh \
    &&     ln -s /opt/conda/etc/profile.d/conda.sh /etc/profile.d/conda.sh \
    &&     echo ". /opt/conda/etc/profile.d/conda.sh" >> ~/.bashrc \
    &&     echo "conda activate base" >> ~/.bashrc \
    &&     find /opt/conda/ -follow -type f -name '*.a' -delete \
    &&     find /opt/conda/ -follow -type f -name '*.js.map' -delete \
    &&     /opt/conda/bin/conda clean -afy

# Configure conda and create nucleoatac env
CMD ["/bin/bash"]
RUN /bin/sh -c set -x                           \
    && conda config --add channels defaults     \
    && conda config --add channels bioconda     \
    && conda config --add channels conda-forge  \
    && conda create --prefix /nucleoatac -y nucleoatac=0.3.4 openssl=1.0    \
    && conda clean -a
ENV PATH=/nucleoatac/bin:/opt/conda/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
ENV PYTHONNOUSERSITE=1
