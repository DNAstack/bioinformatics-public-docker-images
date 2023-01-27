# bioinformatics-public-docker-images

This repository contains public docker images used for workflow execution.

DNAstack's public images built from the files in this repository are hosted [on Dockerhub](https://hub.docker.com/u/dnastack).


## Directory structure

Each tool or set of tools should have its own directory containing at minimum a `build.env` file. If docker definitions for multiple versions of the same tool exist (e.g. samtools version 0.19 and version 1.15), they can be further divided into subdirectories within the `samtools` directory, named by the tool version.

See [the build script documentation](https://github.com/DNAstack/bioinformatics-scripts/tree/master#build-docker-images) for more information on the `build.env` file and how images can be named and tagged.

See [image naming and versioning](#image-naming-and-versioning) for information on how images should be named and versioned.

Example directory structure:
```
bioinformatics-public-docker-images
└── docker
    ├── bcftools_r
    │   ├── build.env
    │   └── Dockerfile
    ├── bwa_samtools
    │   ├── build.env
    │   └── Dockerfile
    ├── samtools
    │   ├── 0.19
    │   │   ├── build.env
    │   │   └── Dockerfile
    │   └── 1.15
    │       ├── build.env
    │       └── Dockerfile
...
    ├── toolA
    │   ├── build.env
    │   └── Dockerfile
    └── toolA_toolB
        ├── build.env
        └── Dockerfile
```


## Image naming and versioning

Images should be named and versioned using this flowchart:

![Docker image naming and versioning flowchart](image_naming_versioning_flowchart.png)


## General best practices

- The Dockerfile should always be named Dockerfile
- Do not write secrets into docker images; if secrets are needed as part of workflow execution, they should be provided as workflow inputs
- Avoid adding large reference files to docker images where possible; provide as workflow inputs
- Do not use the `latest` tag unless you _really_ need things to update automatically; this is prone to breaking
- OS repos and versions of tools in these repos change; prioritize installing tools directly from source
- Make all tool versions environment variables (e.g. `ENV BCFTOOLS_VERSION 1.15.1`) that are controlled within the `build.env` file
- The `Dockerfile` should ideally consume all build arguments defined in the `build.env` file, e.g. by setting them as image environment variables
