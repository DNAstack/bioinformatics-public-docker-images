FROM ubuntu:xenial 

MAINTAINER Karen Fang <karen@dnastack.com>

ARG IMAGE_NAME
ENV IMAGE_NAME "${IMAGE_NAME}"
ARG IMAGE_TAG
ENV IMAGE_TAG "${IMAGE_TAG}"

ARG HTML5VALIDATOR_VERSION
ENV HTML5VALIDATOR_VERSION "${HTML5VALIDATOR_VERSION}"

RUN apt-get -qq update && \
	apt-get -qq install \
		build-essential \
		wget \
		curl \
		zlib1g-dev \
		libreadline-gplv2-dev \
		libncursesw5-dev \
		libssl-dev \
		libsqlite3-dev \
		tk-dev \
		libgdbm-dev \
		libc6-dev \
		libbz2-dev \
		libffi-dev \
		liblzma-dev \
		tabix \
		openjdk-8-jdk

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