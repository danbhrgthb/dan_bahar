## Building the Dockerfile on your local computer with Docker

`docker build -t waafle:1.4.3 -f waafle143_dockerfile .`
 
docker build = do the recipe; -t waafle:1.4.3 = name the finished container; -f waafle143_dockerfile = which dockerfile to use; the . = the files are in this folder.

## Building the Dockerfile on dogen with Podman

Podman is a container engine that works on dogen. Check if Podman is installed with: `podman --version`

First pull the files from GitHub, then build:
```
podman build --format=docker -t waafle_container -f waafle143_dockerfile .
```

podman build = do the recipe; --format=docker = a special Podman flag needed for all runs; -t waafle_container = name the finished container; -f waafle143_dockerfile = which Dockerfile to use; the . = the files are in this folder.
