## Docker Overview

The goal of constructing a Dockerfile within GitHub is that you will then be able to build and run an image based on the Dockerfile. Podman and Docker can both read this file.

## Drafting the yaml

Before proceeding to make a Dockerfile, you must first create a yaml file (link), with all of the environment’s ingredients. One notable change: the name of the environment will always be “base”, regardless of what you are trying to build a Dockerfile for. While dogen can have multiple environments, like waafle_env and baqlava_env, the container only has one environment. Because the container only has one environment, we name it base.
You can name the environment whatever you want on github, but we will be changing its name to base later.

## Drafting the Dockerfile

Below is the waafle Dockerfile (called waafle143_dockerfile, for micromamba 1.4.3). Most Dockerfiles use the same standardized 5-line structure (Baqlava needs a sixth line “RUN pip install baqlava”, because pip can be a bit weird).

```
FROM mambaorg/micromamba:1.4.3
COPY --chown=$MAMBA_USER:$MAMBA_USER waafle_env.yaml /tmp/env.yaml
RUN micromamba install -y -n base -f /tmp/env.yaml
ARG MAMBA_DOCKERFILE_ACTIVATE=1
RUN waafle_search --help
```
 
FROM mambaorg/micromamba:1.4.3
– When making the container, use package manager micromamba 1.4.3.
COPY --chown=$MAMBA_USER:$MAMBA_USER waafle_env.yaml /tmp/env.yaml
– Copies your waafle_env.yaml file into the container under the name env.yaml. /tmp/env.yaml = where it lands inside the container; --chown=$MAMBA_USER:$MAMBA_USER = hands the file to the container’s normal user, as opposed to the admin.
RUN micromamba install -y -n base -f /tmp/env.yaml
– Installs the packages. -y = yes to all prompts; -n base = into the base environment; -f /tmp/env.yaml = using the yaml from above.
ARG MAMBA_DOCKERFILE_ACTIVATE=1
– Switch the base environment ON for the line below.
RUN waafle_search --help
– Try running waafle to ensure that it is actually installed.

## Building the Dockerfile on your local computer


`docker build -t waafle:1.4.3 -f waafle143_dockerfile .`
 
docker build = do the recipe; -t waafle:1.4.3 = name the finished container; -f waafle143_dockerfile = which dockerfile to use; the . = the files are in this folder.

