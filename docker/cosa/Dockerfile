FROM ubuntu:bionic

MAINTAINER Heather Ward <heather@dnastack.com>

ARG IMAGE_NAME
ENV IMAGE_NAME "${IMAGE_NAME}"
ARG IMAGE_TAG
ENV IMAGE_TAG "${IMAGE_TAG}"

RUN apt-get -qq update && \
	apt-get -qq install \
	git \
	python3.8-dev \
	python3-pip \
	python3-setuptools \
	tabix \
	wget \
	make \
	gcc \
	build-essential \
	unzip \
	libz-dev \
	libncurses5-dev \
	libbz2-dev \
	liblzma-dev \
	cmake \
	libjsoncpp-dev \
	autoconf

# CoSA
RUN python3.8 -m pip install pyvcf Cython

ARG COSA_GIT_HASH
ENV COSA_GIT_HASH "${COSA_GIT_HASH}"
RUN cd /opt && git clone https://github.com/PacificBiosciences/CoSA.git
RUN cd /opt/CoSA && \
	git checkout "${COSA_GIT_HASH}" && \
	python3.8 setup.py build && \
	python3.8 setup.py install

# Samtools
ARG SAMTOOLS_VERSION
ENV SAMTOOLS_VERSION "${SAMTOOLS_VERSION}"
RUN wget https://github.com/samtools/samtools/releases/download/${SAMTOOLS_VERSION}/samtools-${SAMTOOLS_VERSION}.tar.bz2 && \
	tar -jxvf samtools-${SAMTOOLS_VERSION}.tar.bz2 --directory /opt/ && \
	rm samtools-${SAMTOOLS_VERSION}.tar.bz2
RUN cd /opt/samtools-${SAMTOOLS_VERSION} && \
	./configure --prefix=/usr/local/ && \
	make && \
	make install

# bcftools
ARG BCFTOOLS_VERSION
ENV BCFTOOLS_VERSION "${BCFTOOLS_VERSION}"
RUN wget https://github.com/samtools/bcftools/releases/download/${BCFTOOLS_VERSION}/bcftools-${BCFTOOLS_VERSION}.tar.bz2 && \
	tar -xvf bcftools-${BCFTOOLS_VERSION}.tar.bz2 --directory /opt && \
	rm bcftools-${BCFTOOLS_VERSION}.tar.bz2
RUN	cd /opt/bcftools-${BCFTOOLS_VERSION} && \
	autoheader && \
	autoconf && \
	./configure && \
	make && \
	make install

# minimap2
ARG MINIMAP2_VERSION
ENV MINIMAP2_VERSION "${MINIMAP2_VERSION}"
RUN wget https://github.com/lh3/minimap2/releases/download/v${MINIMAP2_VERSION}/minimap2-${MINIMAP2_VERSION}_x64-linux.tar.bz2 && \
	tar -jxvf minimap2-${MINIMAP2_VERSION}_x64-linux.tar.bz2 --directory /opt/ && \
	rm minimap2-${MINIMAP2_VERSION}_x64-linux.tar.bz2

ENV PATH $PATH:/opt/minimap2-${MINIMAP2_VERSION}_x64-linux/

# bamtools
ARG BAMTOOLS_GIT_HASH
ENV BAMTOOLS_GIT_HASH "${BAMTOOLS_GIT_HASH}"
RUN cd /opt && git clone https://github.com/pezmaster31/bamtools.git
RUN cd /opt/bamtools && \
	git checkout "${BAMTOOLS_GIT_HASH}" && \
	mkdir build && \
	cd build && \
	cmake -DCMAKE_INSTALL_PREFIX=/usr/local .. && \
	make && \
	make install
