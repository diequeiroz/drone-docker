FROM golang:1.9
WORKDIR /go/src/github.com/drone-plugins/drone-docker
ADD . .
RUN go get -u github.com/golang/dep/cmd/dep && \
    dep ensure && \
    GOOS=linux GOARCH=amd64 CGO_ENABLED=0 go build \
        -tags netgo -o /bin/drone-docker-ecr \
        github.com/drone-plugins/drone-docker/cmd/drone-docker-ecr

FROM plugins/docker:latest
COPY --from=0 /bin/drone-docker-ecr /bin/
ENTRYPOINT ["/usr/local/bin/dockerd-entrypoint.sh", "/bin/drone-docker-ecr"]
