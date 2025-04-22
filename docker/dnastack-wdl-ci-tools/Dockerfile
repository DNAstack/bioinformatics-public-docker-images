ARG BCFTOOLS_VERSION
FROM dnastack/bcftools:${BCFTOOLS_VERSION}
ENV BCFTOOLS_VERSION "${BCFTOOLS_VERSION}"

MAINTAINER Karen Fang <karen@dnastack.com>

ARG IMAGE_NAME
ENV IMAGE_NAME "${IMAGE_NAME}"
ARG IMAGE_TAG
ENV IMAGE_TAG "${IMAGE_TAG}"

ARG FASTAVALIDATOR_VERSION
ENV FASTAVALIDATOR_VERSION "${FASTAVALIDATOR_VERSION}"
ARG YAMLLINT_VERSION
ENV YAMLLINT_VERSION "${YAMLLINT_VERSION}"
ARG HTML5VALIDATOR_VERSION
ENV HTML5VALIDATOR_VERSION "${HTML5VALIDATOR_VERSION}"
ARG PYBIGWIG_VERSION
ENV PYBIGWIG_VERSION "${PYBIGWIG_VERSION}"
ARG PNGCHECK_VERSION
ENV PNGCHECK_VERSION "${PNGCHECK_VERSION}"
ARG XMLLINT_VERSION
ENV XMLLINT_VERSION "${XMLLINT_VERSION}"
ARG QPDF_VERSION
ENV QPDF_VERSION "${QPDF_VERSION}"
ARG HDF5_TOOLS_VERSION
ENV HDF5_TOOLS_VERSION "${HDF5_TOOLS_VERSION}"
ARG IMAGEMAGICK_VERSION
ENV IMAGEMAGICK_VERSION "${IMAGEMAGICK_VERSION}"

RUN apt-get -qq update && \
	apt-get -qq install \
		build-essential \
		wget \
		curl \
		unzip \
		zlib1g-dev \
		libbz2-dev \
		liblzma-dev \
		libpcre3-dev \
		libcurl4-openssl-dev \
		libxml2-dev \
		libssl-dev \
		libfontconfig1-dev \
		libtiff-dev \
		libharfbuzz-dev \
		libfribidi-dev \
		libhdf5-dev \
		libreadline-gplv2-dev \
		libncursesw5-dev \
		libssl-dev \
		libsqlite3-dev \
		tk-dev \
		libgdbm-dev \
		libc6-dev \
		libbz2-dev \
		libffi-dev \
		tabix \
		yamllint \
		python3-dev \
		python3-pip \
		openjdk-8-jdk \
		perl \
		pngcheck \
		libxml2-utils \
		qpdf \
		hdf5-tools \
		gfortran \
		libpcre2-dev \
		imagemagick \
		zip

ARG PYTHON3_VERSION
ENV PYTHON3_VERSION "${PYTHON3_VERSION}"
RUN curl -O https://www.python.org/ftp/python/${PYTHON3_VERSION}/Python-${PYTHON3_VERSION}.tar.xz && \
	tar -xvf Python-${PYTHON3_VERSION}.tar.xz --directory /opt/ && \
	rm Python-${PYTHON3_VERSION}.tar.xz
RUN cd /opt/Python-${PYTHON3_VERSION} && \
	./configure && \
	make && \
	make altinstall

COPY ./requirements.txt /opt/requirements.txt
RUN python3.9 -m pip install -r /opt/requirements.txt

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

# vcftools
ARG VCFTOOLS_VERSION
ENV VCFTOOLS_VERSION "${VCFTOOLS_VERSION}"
RUN wget https://github.com/vcftools/vcftools/releases/download/v${VCFTOOLS_VERSION}/vcftools-${VCFTOOLS_VERSION}.tar.gz && \
	tar -xvf vcftools-${VCFTOOLS_VERSION}.tar.gz --directory /opt && \
	rm vcftools-${VCFTOOLS_VERSION}.tar.gz
RUN	cd /opt/vcftools-${VCFTOOLS_VERSION} && \
	./configure && \
	make && \
	make install

# R
ARG R_VERSION
ENV R_VERSION "${R_VERSION}"
RUN wget https://cran.r-project.org/src/base/R-4/R-${R_VERSION}.tar.gz && \
	tar -zxvf R-${R_VERSION}.tar.gz --directory /opt && \
	rm R-${R_VERSION}.tar.gz

ENV PATH "${PATH}:/opt/R-${R_VERSION}"

WORKDIR /opt/R-${R_VERSION}
RUN ./configure --with-readline=no --with-x=no && \
	make && \
	make install

RUN Rscript -e 'install.packages("SeuratObject", repos="http://cran.r-project.org")'

WORKDIR /opt
