FROM ubuntu:xenial

MAINTAINER Karen Fang <karen@dnastack.com>

RUN apt-get -qq update && \
	apt-get -qq install \
		build-essential \
		wget \
		tar \
		autoconf \
		gzip \
		bzip2 \
		lbzip2 \
		libbz2-dev \
		libcurl4-openssl-dev \
		liblzma-dev \
		ncurses-dev \
		libncurses5-dev \
		zlib1g-dev \
		libbz2-dev \
		jq \
		curl && \
	rm -rf /var/lib/apt/lists/*

# samtools
ENV SAMTOOLS_VERSION 1.16.1
RUN wget https://github.com/samtools/samtools/releases/download/${SAMTOOLS_VERSION}/samtools-${SAMTOOLS_VERSION}.tar.bz2 && \
	tar -jxvf samtools-${SAMTOOLS_VERSION}.tar.bz2 --directory /opt/ && \
	rm samtools-${SAMTOOLS_VERSION}.tar.bz2

RUN 	cd /opt/samtools-${SAMTOOLS_VERSION} && \
	autoheader && \
	autoconf && \
	./configure && \
	make && \
	make install

ENV PATH $PATH:/opt/samtools-${SAMTOOLS_VERSION}

# bcftools
ENV BCFTOOLS_VERSION 1.16
RUN wget https://github.com/samtools/bcftools/releases/download/${BCFTOOLS_VERSION}/bcftools-${BCFTOOLS_VERSION}.tar.bz2 && \
	tar -xvf bcftools-${BCFTOOLS_VERSION}.tar.bz2 --directory /opt && \
	rm bcftools-${BCFTOOLS_VERSION}.tar.bz2

RUN	cd /opt/bcftools-${BCFTOOLS_VERSION} && \
	autoheader && \
	autoconf && \
	./configure && \
	make && \
	make install

ENV PATH $PATH:/opt/bcftools-${BCFTOOLS_VERSION}

# TRGT
ENV TRGT_VERSION v0.3.2
RUN wget https://github.com/PacificBiosciences/trgt/releases/download/${TRGT_VERSION}/trgt-${TRGT_VERSION}-linux_x86_64.gz && \
	gzip -d trgt-${TRGT_VERSION}-linux_x86_64.gz

RUN	mkdir /opt/trgt-${TRGT_VERSION}-linux_x86_64 && \
	mv ./trgt-${TRGT_VERSION}-linux_x86_64 /opt/trgt-${TRGT_VERSION}-linux_x86_64/trgt-${TRGT_VERSION}-linux_x86_64 && \
	cd /opt/trgt-${TRGT_VERSION}-linux_x86_64 && \
	chmod +x trgt-${TRGT_VERSION}-linux_x86_64

RUN ln -s /opt/trgt-${TRGT_VERSION}-linux_x86_64/trgt-${TRGT_VERSION}-linux_x86_64 /usr/local/bin/trgt

# TRVZ
ENV TRVZ_VERSION v0.3.2
RUN wget https://github.com/PacificBiosciences/trgt/releases/download/${TRVZ_VERSION}/trvz-${TRVZ_VERSION}-linux_x86_64.gz && \
	gzip -d trvz-${TRVZ_VERSION}-linux_x86_64.gz 

RUN	mkdir /opt/trvz-${TRVZ_VERSION}-linux_x86_64 && \
	mv ./trvz-${TRVZ_VERSION}-linux_x86_64 /opt/trvz-${TRVZ_VERSION}-linux_x86_64/trvz-${TRVZ_VERSION}-linux_x86_64 && \
	cd /opt/trvz-${TRVZ_VERSION}-linux_x86_64 && \
	chmod +x trvz-${TRVZ_VERSION}-linux_x86_64

RUN ln -s /opt/trvz-${TRVZ_VERSION}-linux_x86_64/trvz-${TRVZ_VERSION}-linux_x86_64 /usr/local/bin/trvz
