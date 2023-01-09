FROM ubuntu:bionic

MAINTAINER Heather Ward <heather@dnastack.com>

ARG IMAGE_NAME
ENV IMAGE_NAME "${IMAGE_NAME}"
ARG IMAGE_TAG
ENV IMAGE_TAG "${IMAGE_TAG}"

RUN apt-get -qq update && \
	apt-get -qq install \
	curl \
	wget \
	unzip \
	ncbi-blast+ \
	snp-sites \
	bcftools \
	vcftools \
	openjdk-8-jre \
	gawk

# mview
ARG MVIEW_VERSION
ENV MVIEW_VERSION "${MVIEW_VERSION}"
RUN wget https://github.com/desmid/mview/archive/v${MVIEW_VERSION}.tar.gz && \
	tar -zxvf v${MVIEW_VERSION}.tar.gz --directory /opt/ && \
	rm v${MVIEW_VERSION}.tar.gz
ENV PERL5LIB=$PERL5LIB:/opt/mview-${MVIEW_VERSION}/lib/
RUN ln -s /opt/mview-${MVIEW_VERSION}/bin/mview /usr/local/bin/

COPY ./scripts/* /usr/local/bin/
