FROM ubuntu:xenial

MAINTAINER Heather Ward <heather@dnastack.com>

ARG IMAGE_NAME
ENV IMAGE_NAME "${IMAGE_NAME}"
ARG IMAGE_TAG
ENV IMAGE_TAG "${IMAGE_TAG}"

RUN apt-get -qq update \
	&& apt-get -qq install \
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
		liblzma-dev \
	&& rm -rf /var/lib/apt/lists/*

# bwa
ARG BWA_VERSION
ENV BWA_VERSION "${BWA_VERSION}"
RUN wget https://github.com/lh3/bwa/archive/${BWA_VERSION}.tar.gz && \
	tar -zxvf ${BWA_VERSION}.tar.gz --directory /opt && \
	rm ${BWA_VERSION}.tar.gz

WORKDIR /opt/bwa-${BWA_VERSION}
RUN	cd /opt/bwa-${BWA_VERSION} && \
	make && \
	ln -s /opt/bwa-${BWA_VERSION}/bwa /usr/local/bin/

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
