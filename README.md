[![](https://images.microbadger.com/badges/image/ecliptik/docker-siege.svg)](https://microbadger.com/images/ecliptik/docker-siege "Get your own image badge on microbadger.com")

#Usage
## Running Container as a Command

This is a public version of the Siege container used for load testing at [Demandbase](https://www.demandbase.com).

To run this container using the [ecliptik/docker-siege](https://hub.docker.com/r/ecliptik/docker-siege/) image stored in Docker Hub that is automatically built whenever this github repository is updated. The [Dockerfile](Dockerfile) has a default `ENTRYPOINT` of `siege` and all arguments passed after the container image will pass to `siege`. The default argument is `--help`.

## Running Container With Local Configuration

To skip the bundled configuration files in the image, and use local files in the current directoy, bind mount it to `/app` using the `-v` flag.

For example using this repository and you want to create a URL list to pass to siege called `urls.txt` without having to re-build the container image,

```
docker pull ecliptik/docker-siege
docker run -it --rm -v $(pwd):/app ecliptik/docker-siege -c 50 -f /app/urls.txt -R /app/siege.conf
```

The `-v $(pwd):/app` will bind mount your current directory to `/app` within the container, letting you use local files.

## Running in a Jenkins Job

Runnig this container using the image in Docker Hub as a Jenkins job requires not including the `-t` option, otherwise Jenkins will give an error.

## Updating Docker Image

To update the version fo Siege, find the latest version from the [Siege Downloads](http://download.joedog.org/siege/) page and in the [Dockerfile](Dockerfile) update the `SIEGE_VERSION` variable and re-build,

```
docker build -t ecliptik/docker-siege .
```
