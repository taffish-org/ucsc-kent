FROM ghcr.io/taffish-org/debian:12

LABEL maintainer="taffish@163.com"

WORKDIR /root

RUN apt-get update && \
    apt-get install -y curl git gcc g++ make \
                       libpng-dev uuid-dev libmariadb-dev libmariadb-dev-compat \
                       libcurl4-openssl-dev libbz2-dev liblzma-dev && \
    cd / && \
    curl -LO https://github.com/ucscGenomeBrowser/kent-core/archive/refs/tags/v486.tar.gz && \
    tar -zxvf /v486.tar.gz && rm /v486.tar.gz && \
    cd /kent-core-486/ && \
    git clone --recursive https://github.com/samtools/htslib.git && \
    cd /kent-core-486/htslib/    && make -j$(nproc) && make install && \
    cd /kent-core-486/           && make -j$(nproc) || true && \
    cd /kent-core-486/src/lib/   && make -j$(nproc) && \
    cd /kent-core-486/src/utils/ && make -j$(nproc) && \
    mv /root/bin/* /kent-core-486/bin/
    
ENV PATH=/kent-core-486/bin:${PATH}
ENV PATH=/kent-core-486/bin/aarch64:${PATH}
ENV PATH=/kent-core-486/bin/x86_64:${PATH}
ENV PATH=/kent-core-486/bin/scripts:${PATH}
ENV PATH=/kent-core-486/src/utils:${PATH}

ENV TAFFISH_ENV=TAFFISH
ENV TAFFISH_NAME=ucsc-kent
