# drone-docker

This is an opinionated update on [drone-plugins/drone-docker](https://github.com/drone-plugins/drone-docker) ecr plugin, which does the following:

* make we use the host daemon by default (PLUGIN_DAEMON_OFF = true)
* turns off image cleanup at the end of the build (PLUGIN_PURGE = false)
* activate debug logs (PLUGIN_DEBUG = true)

For more information please see the original [documentation](http://plugins.drone.io/drone-plugins/drone-ecr/).
 
## Build

Build the binary with the following commands:

```
GOOS=linux GOARCH=amd64 CGO_ENABLED=0 go build -tags netgo
```

## Docker

Build the Docker image with the following commands:

```
docker build --rm=true -f docker/Dockerfile -t quintoandar/drone-ecr .
```

## Usage

Execute from the working directory:

```
docker run --rm \
  -e PLUGIN_TAG=latest \
  -e PLUGIN_REPO=octocat/hello-world \
  -e DRONE_COMMIT_SHA=d8dbe4d94f15fe89232e0402c6e8a0ddf21af3ab \
  -v $(pwd):$(pwd) \
  -w $(pwd) \
  --privileged \
  plugins/docker --dry-run
```
