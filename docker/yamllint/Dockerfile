FROM ubuntu:xenial 

MAINTAINER Karen Fang <karen@dnastack.com>

ARG IMAGE_NAME
ENV IMAGE_NAME "${IMAGE_NAME}"
ARG IMAGE_TAG
ENV IMAGE_TAG "${IMAGE_TAG}"

ARG YAMLLINT_VERSION
ENV YAMLLINT_VERSION "${YAMLLINT_VERSION}"

RUN apt-get -qq update && \
	apt-get -qq install \
		build-essential \
		wget \
		unzip \
		yamllint \
		python3-dev \
		python3-pip