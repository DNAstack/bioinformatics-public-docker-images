FROM ubuntu:bionic

MAINTAINER Heather Ward <heather@dnastack.com>

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

# mview 1.67
ENV MVIEW_VERSION 1.67
RUN wget https://github.com/desmid/mview/archive/v${MVIEW_VERSION}.tar.gz && \
	tar -zxvf v${MVIEW_VERSION}.tar.gz --directory /opt/ && \
	rm v${MVIEW_VERSION}.tar.gz
ENV PERL5LIB=$PERL5LIB:/opt/mview-${MVIEW_VERSION}/lib/
RUN ln -s /opt/mview-${MVIEW_VERSION}/bin/mview /usr/local/bin/

COPY ./scripts/* /usr/local/bin/
