FROM continuumio/miniconda3:4.10.3 AS condabuild

MAINTAINER Heather Ward <heather@dnastack.com>

ENV ARTIC_VERSION 1.3.0
RUN wget https://github.com/connor-lab/ncov2019-artic-nf/archive/refs/tags/v${ARTIC_VERSION}.tar.gz && \
	tar -zxvf v${ARTIC_VERSION}.tar.gz --directory /opt && \
	rm v${ARTIC_VERSION}.tar.gz

WORKDIR /opt/ncov2019-artic-nf-${ARTIC_VERSION}

RUN /opt/conda/bin/conda install mamba -c conda-forge && \
	/opt/conda/bin/mamba env create -f environments/nanopore/environment.yml

RUN apt-get -qq update && \
	apt-get -qq install \
		tabix \
		samtools \
		xxd \
		zip

COPY requirements.txt /opt/requirements.txt
RUN python3 -m pip install -r /opt/requirements.txt

ENV SCHEME_REPO /opt/artic-ncov2019

RUN git clone https://github.com/artic-network/artic-ncov2019.git "$SCHEME_REPO" && \
	for reference in $(find "${SCHEME_REPO}/primer_schemes/nCoV-2019" -name "nCoV-2019.reference.fasta"); do \
		samtools faidx "${reference}"; \
	done

COPY ./scripts/* /usr/local/bin/

ENV PATH=/opt/conda/envs/artic/bin:/opt/ncov2019-artic-nf-${ARTIC_VERSION}/bin:$PATH
