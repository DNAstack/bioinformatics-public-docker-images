FROM ubuntu:xenial

MAINTAINER Heather Ward <heather@danstack.com>

ARG IMAGE_NAME
ENV IMAGE_NAME "${IMAGE_NAME}"
ARG IMAGE_TAG
ENV IMAGE_TAG "${IMAGE_TAG}"

RUN apt-get -qq update && \
	apt-get -qq install \
		wget \
		jq

ARG NEXTCLADE_VERSION
ENV NEXTCLADE_VERSION "${NEXTCLADE_VERSION}"
RUN mkdir -p /opt/nextclade && \
	wget -O /opt/nextclade/nextclade https://github.com/nextstrain/nextclade/releases/download/${NEXTCLADE_VERSION}/nextclade-x86_64-unknown-linux-gnu && \
	chmod +x /opt/nextclade/nextclade
RUN ln -s /opt/nextclade/nextclade /usr/local/bin

ENV MONKEYPOX_DATASET /data/monkeypox
RUN mkdir -p ${MONKEYPOX_DATASET} && \
	nextclade dataset get --name 'MPXV' --output-dir ${MONKEYPOX_DATASET}
