FROM ubuntu:23.10 AS hmmer-builder

RUN apt-get update && apt-get install -y \
    git \
    python3 \
    python3-pip \
    wget \
    curl \
    unzip \
    htop \
    vim

RUN wget http://eddylab.org/software/hmmer/hmmer.tar.gz

RUN tar zxf hmmer.tar.gz

WORKDIR hmmer-3.4

RUN ./configure --prefix /usr/local

RUN make

FROM ubuntu:23.10 AS prodigal-builder

RUN apt-get update && apt-get install -y \
    build-essential \
    git \
    zlib1g-dev

RUN git clone https://github.com/hyattpd/Prodigal
WORKDIR Prodigal
RUN make

FROM debian:latest 

RUN apt-get update && apt-get install -y \
    git \
    gzip \
    gcc \
    make \
    python3 \
    python3-biopython \
    python3-matplotlib \
    python3-numpy \
    python3-pandas \
    python3-pip \
    python3-seaborn \
    python3-sklearn \
    tar \
    wget

COPY --from=prodigal-builder /Prodigal /
COPY --from=hmmer-builder /hmmer-3.4 /

RUN git clone https://github.com/AnantharamanLab/VIBRANT
RUN chmod -R 777 VIBRANT

WORKDIR VIBRANT/databases 
RUN python3 VIBRANT_setup.py