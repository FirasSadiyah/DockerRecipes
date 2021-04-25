FROM bioconductor/bioconductor_docker
LABEL version="1.0" maintainer="Firas Sadiyah <Firas [dot] Sadiyah [at] GMail>"

RUN apt-get update \
&& apt-get install -y \
curl \
wget \
libboost-all-dev \
libudunits2-dev \
gawk

# Install miniconda
RUN wget https://repo.continuum.io/miniconda/Miniconda2-latest-Linux-x86_64.sh \
&& bash Miniconda2-latest-Linux-x86_64.sh -b -p /opt/miniconda2 \
&& /opt/miniconda2/bin/conda config --add channels bioconda \
&& /opt/miniconda2/bin/conda config --add channels defaults \
&& /opt/miniconda2/bin/conda config --add channels conda-forge

# Install software required for chipseq pipeline with bioconda
RUN /opt/miniconda2/bin/conda install -c bioconda deeptools \
&& /opt/miniconda2/bin/conda install -c bioconda wiggletools \
&& /opt/miniconda2/bin/conda install -c bioconda ucsc-bedclip \
&& /opt/miniconda2/bin/conda install -c bioconda ucsc-bedgraphtobigwig \
&& /opt/miniconda2/bin/conda install -c bioconda bedops \
&& /opt/miniconda2/bin/conda install -c bioconda bedtools

# Update path
ENV PATH "/opt/miniconda2/bin:$PATH"
ENV PATH "/usr/local/bin:$PATH"
