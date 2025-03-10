# DinD with nvidia-docker

Use nvidia-docker inside a container.


## Requirements

[nvidia container toolkit](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/latest/install-guide.html) is required on the host machine.


## Building image

You can either pull the image `mrdavoy/dind:nvidia-docker` or build the image by yourself with the following command:  
```shell
  $ docker build -t dind:nvidia-docker .
```

CUDA version and be specified with --build-arg:
```shell
  $ docker build -t dind:nvidia-docker --build-arg CUDA_IMAGE=nvidia/cuda:9.0-runtime
```


## Running the dind:nvidia-docker container

The usage of the container is the same as the [official dind image](https://hub.docker.com/_/docker), except that you have to run it in a `nvidia` runtime.

Here is an example.
First, run the container on the host machine.
```shell
  $ DIND=$(docker run --privileged -d --runtime=nvidia dind:nvidia-docker)
  $ docker exec -it $DIND /bin/bash
```
Now we have a shell in the dind container. Inside this container, you can run any container that requires `nvidia` runtime.

You can also connect a second container to `dind:nvidia-docker`. Refer to [official dind image](https://hub.docker.com/_/docker) to read the steps.


## Acknowledgement
Forked from [https://github.com/divergent3d/dind-nvidia-docker]{https://github.com/divergent3d/dind-nvidia-docker}
The dind part of this Dockerfile is copied from [https://github.com/docker-library/docker/tree/master/18.09/dind](https://github.com/docker-library/docker/tree/master/18.09/dind)
