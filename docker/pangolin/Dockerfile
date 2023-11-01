ARG MINICONDA3_VERSION
FROM continuumio/miniconda3:${MINICONDA3_VERSION}
ENV MINICONDA3_VERSION "${MINICONDA3_VERSION}"

MAINTAINER Heather Ward <heather@dnastack.com>

ARG IMAGE_NAME
ENV IMAGE_NAME "${IMAGE_NAME}"
ARG IMAGE_TAG
ENV IMAGE_TAG "${IMAGE_TAG}"

ARG PANGOLIN_VERSION
ENV PANGOLIN_VERSION "${PANGOLIN_VERSION}"

RUN apk update && \
	apk add git bash

RUN wget https://github.com/cov-lineages/pangolin/archive/refs/tags/v${PANGOLIN_VERSION}.tar.gz && \
	tar -zxvf v${PANGOLIN_VERSION}.tar.gz --directory /opt && \
	rm v${PANGOLIN_VERSION}.tar.gz

WORKDIR /opt/pangolin-${PANGOLIN_VERSION}

# Python 3.8.5 already installed along with recent version of pip
# so remove Python and pip deps from environment.yml before installation
# Cannot remove pip since pango-designation v1.23.1; must specify version
RUN sed -i "$(grep -n 'python>=3.7' ./environment.yml | cut -f1 -d:)d" ./environment.yml

# Install the conda environment
RUN conda env create --quiet -f ./environment.yml && conda clean -a

# Add conda installation dir to PATH (instead of doing 'conda activate')
ENV PATH /opt/conda/envs/pangolin/bin:$PATH

# Install Pangolin
RUN pip install . && rm -rf /root/.cache/pip
RUN pangolin --version &> /pangolin-version.txt

# Dump the details of the installed packages to a file for posterity
RUN conda env export --name pangolin > /pangolin.yml
