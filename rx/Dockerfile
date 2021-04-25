FROM rocker/tidyverse:latest
LABEL version="1.0" maintainer="Firas Sadiyah <Firas [dot] Sadiyah [at] GMail>"

## Some of the R packages depend on libraries not already installed
RUN apt-get update        \
    && apt-get install -y \
    libgsl0-dev           \
    libmagick++-dev       \
    libudunits2-dev       \
    gdal-bin              \
    libgdal-dev

## Install the following R packages - big download so increase timeout to 120s
RUN R -e "if (!requireNamespace('BiocManager', quietly = TRUE)) install.packages('BiocManager')"
RUN R -e "options(timeout = 180)" -e "BiocManager::install('BSgenome.Mmusculus.UCSC.mm9')"
RUN R -e "options(timeout = 120)" -e "BiocManager::install('TxDb.Mmusculus.UCSC.mm9.knownGene')"
RUN R -e "options(timeout = 180)" -e "BiocManager::install('BSgenome.Mmusculus.UCSC.mm10')"
RUN R -e "options(timeout = 120)" -e "BiocManager::install('TxDb.Mmusculus.UCSC.mm10.knownGene')"
RUN R -e "options(timeout = 180)" -e "BiocManager::install('BSgenome.Hsapiens.UCSC.hg19')"
RUN R -e "options(timeout = 120)" -e "BiocManager::install('TxDb.Hsapiens.UCSC.hg19.knownGene')"
RUN R -e "options(timeout = 180)" -e "BiocManager::install('BSgenome.Hsapiens.UCSC.hg38')"
RUN R -e "options(timeout = 120)" -e "BiocManager::install('TxDb.Hsapiens.UCSC.hg38.knownGene')"
RUN rm -rf /tmp/downloaded_packages/ /tmp/*.rds


## Install the following packages from Bioconductor
RUN install2.r --error BiocManager                                       \
&& Rscript -e 'requireNamespace("BiocManager"); BiocManager::install();' \
&& Rscript -e 'requireNamespace("BiocManager"); BiocManager::install(c("GenomicRanges", "deseq2", "diffbind", "csaw", "edgeR", "purrr", "PCAtools", "qrqc", "rtracklayer", "GenomicFiles", "GenomicAlignments", "BSgenome", "Biostrings", "GenomicInteractions",  "GenomicAlignments", "Rsamtools"));' \
&& rm -rf /tmp/downloaded_packages/ /tmp/*.rds

## Install the following packages from CRAN
RUN rm -rf /tmp/*.rds  \
&&  install2.r --error \
    cowplot            \
    bedr               \
    VennDiagram        \
    eulerr             \
    magrittr           \
    reshape2           \
    statmod            \
    furrr              \
    matrixStats        \
    aws.s3             \
    scales             \
    ggrepel            \
    caTools            \
    GGally             \
    ROCR               \
    readr              \
&&  rm -rf /tmp/downloaded_packages/ /tmp/*.rds


## Install population genetics packages from Github
## RUN installGithub.r \
##     repo/package \
## & rm -rf /tmp/downloaded_packages/ /tmp/*.rds
