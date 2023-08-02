FROM ubuntu:xenial

MAINTAINER Jesse Wolf <jesse@dnastack.com>

ARG IMAGE_NAME
ENV IMAGE_NAME "${IMAGE_NAME}"
ARG IMAGE_TAG
ENV IMAGE_TAG "${IMAGE_TAG}"

RUN apt-get -qq update && \
	apt-get -qq install \
	g++ \
	make \
	libz-dev \
	python-minimal \
	libreadline-dev \
	wget \
	unzip

# Add mothur
ARG MOTHUR_VERSION
ENV MOTHUR_VERSION "${MOTHUR_VERSION}"
RUN wget https://github.com/mothur/mothur/archive/refs/tags/v${MOTHUR_VERSION}.tar.gz && \
	tar -zxvf v${MOTHUR_VERSION}.tar.gz --directory /opt && \
	rm v${MOTHUR_VERSION}.tar.gz
RUN cd /opt/mothur-${MOTHUR_VERSION} && \
	make && \
	make install

RUN wget https://github.com/mothur/mothur/releases/download/v${MOTHUR_VERSION}/Mothur.tools_linux.zip && \
	unzip Mothur.tools_linux.zip -d /opt/mothur-${MOTHUR_VERSION} && \
	rm Mothur.tools_linux.zip && \
	cd /opt/mothur-${MOTHUR_VERSION}/tools && \
	mv * ../

# Add mothur folder to the PATH
ENV PATH="/opt/mothur-1.48.0/:${PATH}"
