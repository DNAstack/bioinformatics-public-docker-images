FROM continuumio/miniconda3:4.9.2

# Based on https://github.com/jaleezyy/covid-19-signal/blob/master/resources/Dockerfile_pipeline
MAINTAINER Heather Ward <heather@dnastack.com>

ARG IMAGE_NAME
ENV IMAGE_NAME "${IMAGE_NAME}"
ARG IMAGE_TAG
ENV IMAGE_TAG "${IMAGE_TAG}"

RUN apt-get -qq --allow-releaseinfo-change update && \
	apt-get -qq install \
		curl \
		wget \
		git \
		build-essential \
		libtbb2 \
		tabix \
		bcftools \
		zip \
		xxd && \
	conda init bash

# Download required datasets; these are included as part of the Dockerfile to ensure AWS's EBS does not get overwhelmed at large sample numbers
# N.B. that this makes the final Docker image ~10 GB
RUN mkdir /data
RUN	wget https://storage.googleapis.com/dnastack-data-ingestion-storage/resources/Kraken2.tar.gz && \
	tar -zxvf Kraken2.tar.gz --directory /data && \
	rm Kraken2.tar.gz
RUN wget https://storage.googleapis.com/dnastack-data-ingestion-storage/resources/composite_human_viral_reference.tar.gz && \
	tar -zxvf composite_human_viral_reference.tar.gz --directory /data && \
	rm composite_human_viral_reference.tar.gz

ENV KRAKEN2_DB /data/Kraken2/db
ENV COMPOSITE_REFERENCE /data/composite_human_viral_reference/composite_human_viral_reference.fna

# snakemake and system dependencies
RUN conda create --name snakemake --channel conda-forge --channel bioconda snakemake==6.0.5 pandas

ENV SIGNAL_VERSION "${IMAGE_TAG}"
RUN wget https://github.com/jaleezyy/covid-19-signal/archive/refs/tags/v${SIGNAL_VERSION}.tar.gz && \
	tar -zxvf v${SIGNAL_VERSION}.tar.gz --directory /opt && \
	rm v${SIGNAL_VERSION}.tar.gz

WORKDIR /opt/covid-19-signal-${SIGNAL_VERSION}

# install all snakemake rule conda envs using dummy snakemake file
COPY ./dependencies resources/dependencies
RUN conda run \
	-n snakemake snakemake \
	--verbose \
	--use-conda \
	--conda-prefix=$HOME/.snakemake \
	-s resources/dependencies \
	--cores 8

COPY ./scripts/* /usr/local/bin/
