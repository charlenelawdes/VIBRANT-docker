FROM debian:bullseye
FROM ghcr.io/charlenelawdes/hmmer-docker AS hmmer-builder
FROM ghcr.io/charlenelawdes/prodigal-docker AS prodigal-builder
FROM ghcr.io/charlenelawdes/sklearn-docker AS sklearn-builder

RUN apt-get update && apt-get install -y \
    git \
    gcc \
    python3 \
    cython3 \
    python3-biopython \
    python3-matplotlib \
    python3-pandas \
    python3-seaborn \
    python3-pip \
    wget


COPY --from=hmmer-builder /usr/local/bin/ /usr/local/bin/
COPY --from=prodigal-builder /usr/local/bin/ /usr/local/bin/

RUN pip3 install -U scikit-learn==0.21.3
RUN git clone https://github.com/AnantharamanLab/VIBRANT
RUN chmod -R 777 VIBRANT

WORKDIR /VIBRANT

RUN python3 databases/VIBRANT_setup.py
