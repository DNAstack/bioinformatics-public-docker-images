# TAG gcr.io/cool-benefit-817/bcftools:1.15.1
FROM ubuntu:bionic

RUN apt-get -qq update && \
	apt-get -qq install \
	wget \
	curl \
	make \
	gcc \
	build-essential \
	libz-dev \
	libbz2-dev \
	liblzma-dev \
	libcurl4-openssl-dev \
	libssl-dev \
	tabix \
	apt-transport-https \
	ca-certificates \
	gnupg \
	bedops

# gcloud cli
RUN echo "deb [signed-by=/usr/share/keyrings/cloud.google.gpg] http://packages.cloud.google.com/apt cloud-sdk main" | tee -a /etc/apt/sources.list.d/google-cloud-sdk.list && \
	curl https://packages.cloud.google.com/apt/doc/apt-key.gpg \
	| apt-key --keyring /usr/share/keyrings/cloud.google.gpg  add - && \
	apt-get -qq update && \
	apt-get -qq install \
	google-cloud-cli

ENV BCFTOOLS_VERSION 1.15.1

RUN wget https://github.com/samtools/bcftools/releases/download/${BCFTOOLS_VERSION}/bcftools-${BCFTOOLS_VERSION}.tar.bz2 && \
	tar -jxvf bcftools-${BCFTOOLS_VERSION}.tar.bz2 --directory /opt && \
	rm bcftools-${BCFTOOLS_VERSION}.tar.bz2

RUN cd /opt/bcftools-${BCFTOOLS_VERSION} && \
	./configure && \
	make && \
	make install
