FROM golang:1.12-alpine

# We aren't using the /go directory defined in base image
WORKDIR /data
ENV HOME /data
ENV GOPATH /data/go

ENV npm_config_cache=/data/npm_cache

# Create links based on passed in ALL_ARCH
ARG ALL_ARCH
ENV ALL_ARCH ${ALL_ARCH}
RUN for ARCH in ${ALL_ARCH}; do \
      ln -s -f "/data/std/${ARCH}" "/usr/local/go/pkg/linux_${ARCH}_static" ; \
    done

RUN apk update && apk upgrade && apk add --no-cache git nodejs bash npm

# Install any binaries in to /usr/local/bin instead of /go/bin as we will mask
# /go/bin when doing real builds.
RUN GOPATH=/tmp GOBIN=/usr/local/bin go get -u github.com/jteeuwen/go-bindata/...
RUN GOPATH=/tmp GOBIN=/usr/local/bin go get github.com/tools/godep
