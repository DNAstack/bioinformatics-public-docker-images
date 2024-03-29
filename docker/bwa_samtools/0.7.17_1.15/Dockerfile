FROM ubuntu:xenial

MAINTAINER Karen Fang <karen@dnastack.com>

ARG IMAGE_NAME
ENV IMAGE_NAME "${IMAGE_NAME}"
ARG IMAGE_TAG
ENV IMAGE_TAG "${IMAGE_TAG}"

RUN apt-get -qq update && \
	apt-get -qq install \
		build-essential \
		wget \
		tar \
		gzip \
		tabix \
		lbzip2 \
		make \
		autoconf \
		libncurses5-dev \
		zlib1g-dev \
		libbz2-dev \
		liblzma-dev && \
	rm -rf /var/lib/apt/lists/*

# bwa
ARG BWA_VERSION
ENV BWA_VERSION "${BWA_VERSION}"
RUN wget https://github.com/lh3/bwa/releases/download/v${BWA_VERSION}/bwa-${BWA_VERSION}.tar.bz2 && \
	tar -xvf bwa-${BWA_VERSION}.tar.bz2 --directory /opt && \
	rm bwa-${BWA_VERSION}.tar.bz2
RUN	cd /opt/bwa-${BWA_VERSION} && \
	make
ENV PATH $PATH:/opt/bwa-${BWA_VERSION}

# samtools
ARG SAMTOOLS_VERSION
ENV SAMTOOLS_VERSION "${SAMTOOLS_VERSION}"
RUN wget https://github.com/samtools/samtools/releases/download/${SAMTOOLS_VERSION}/samtools-${SAMTOOLS_VERSION}.tar.bz2 && \
	tar -xvf samtools-${SAMTOOLS_VERSION}.tar.bz2 --directory /opt && \
	rm samtools-${SAMTOOLS_VERSION}.tar.bz2
RUN	cd /opt/samtools-${SAMTOOLS_VERSION} && \
	autoheader && \
	autoconf -Wno-syntax && \
	./configure && \
	make && \
	make install
