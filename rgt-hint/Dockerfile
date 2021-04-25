FROM ubuntu:20.04
LABEL version="1.0" maintainer="Firas Sadiyah <Firas [dot] Sadiyah [at] GMail>"

# Set the time zone
ENV TZ=Europe/London
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

# Set the environment
ENV LANG=C.UTF-8 LC_ALL=C.UTF-8

# Update the system and install python3 and pip3
RUN apt-get update         \
    && apt-get install -y  \
       zlib1g-dev libbz2-dev liblzma-dev \
       libkrb5-3 gdebi wget  locales     \
       texlive-font-utils  \
       python3 python3-pip \
    && apt-get clean

# Install to get add-apt-repository
RUN apt-get install -y software-properties-common
# Install libpng12 from the following repo
RUN add-apt-repository ppa:linuxuprising/libpng12 \
    && apt-get update \
    && apt-get install -y libpng12-0 \
    && apt-get clean

# Install RGT
RUN pip3 install cython numpy scipy
RUN pip3 install RGT==0.13.1

# set RGTDATA
ENV RGTDATA=~/rgtdata
