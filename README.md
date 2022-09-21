# bioinformatics-public-docker-images

This repository contains public docker images used for workflow execution.

DNAstack's public images built from the files in this repository are hosted [on Dockerhub](https://hub.docker.com/u/dnastack).


## Directory structure

Each tool or set of tools should have its own directory. This directory should have the same name as the docker image that is built from it, excluding the container registry. Within the directory should be a subdirectory specifying the image version, within which the Dockerfile and other required files can be found.

The directory structure determines the name and version tag for the resulting image. For example, the image built from the Dockerfile located at the path `bioinformatics-public-docker-images/${tool}/${version}/Dockerfile` will be tagged as `dnastack/${tool}:${version}`.

See [image naming and versioning](#image-naming-and-versioning) for information on how images should be named and versioned.

Different versions of a tool or set of tools should be nested under the tool/image name.

```
bioinformatics-public-docker-images
├── samtools
│  └── 1.15
│      └── Dockerfile
├── bcftools_r
│   ├── 1.1.5_4.2.1
│   │   └── Dockerfile
│   └── 1.1.6_4.2.1
│       └── Dockerfile
├── bwa_samtools
│   └── 0.7.17_1.16.1
│       └── Dockerfile
...
├── tool
│   └── version
│       └── Dockerfile
└── toolA_toolB
    └── versionA_versionB
        └── Dockerfile
```


## Image naming and versioning

Follow this handy flowchart!

![Docker image naming and versioning flowchart](image_naming_versioning_flowchart.png)


## General best practices

- The Dockerfile should always be named Dockerfile
- Do not write secrets into docker images; if secrets are needed as part of workflow execution, they should be provided as workflow inputs
- Avoid adding large reference files to docker images where possible; provide as workflow inputs
- Do not use the `latest` tag unless you _really_ need things to update automatically; this is prone to breaking
- OS repos and versions of tools in these repos change; prioritize installing tools directly from source
