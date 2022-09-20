# bioinformatics-public-docker-images

## The `bioinformatics-public-docker-images` repository

The `docker` repository contains one subdirectory for each docker image that exists for all projects. This subdirectory should be named the same as the docker image that is built from it, excluding the registry hostname and the tag.

e.g. the Dockerfile for an image tagged `hkeward/samtools:0.19` should be in a directory titled `samtools/0.19`; an image tagged `hkeward/some/path/samtools:1.15` should likewise be in a directory named `samtools/1.15`.

```
`bioinformatics-public-docker-images` repo
└── samtools
    └── 1.15
        └── Dockerfile
└── bcftools
    └── 1.16
	    └── Dockerfile

...

└── tool
    └── version
        └── Dockerfile
```

If multiple versions of a tool have separate docker images, they should be nested under the tool/image name, e.g.

```
`bioinformatics-public-docker-images` repo
└── samtools
    ├── 0.19
    │   └── Dockerfile
    └── 1.15
        └── Dockerfile
```

## Image versioning

There are two versioning schemes in place:

1. If an image contains a single tool, e.g. samtools, the version should be set to the tool version.
2. If an image contains multiple tools, [semantic versioning](https://semver.org/) should be used.


### Dockerfiles

The first line of every Dockerfile should follow the format:

```
# TAG container_registry/tool_name:version
```

Secrets should never be written into docker images. If secrets are needed as part of workflow execution, they should be provided as workflow inputs.

Adding large reference files to docker containers should be avoided where possible; provide them as workflow inputs.


## Example directory structure

```
└── samtools
    └── 0.19
        └── Dockerfile
    └── 1.15
        └── Dockerfile
└── bcftools
    └── 1.16
        └── Dockerfile
```

## Example GitHub repo path

The version should be tag of docker image.

`/DNAstack/bioinformatics-public-docker-image/tool/version/Dockerfile`

## Example docker image path

The tag should be version of tool.

`~{container_registry}/tool:version`
