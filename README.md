# Golang Container

[![GitHub](https://img.shields.io/github/license/MarceloHMariano/golang-container)](LICENSE)
[![Docker Cloud Automated build](https://img.shields.io/docker/cloud/automated/marcelohmariano/golang)](https://hub.docker.com/r/marcelohmariano/golang)
[![Docker Cloud Build Status](https://img.shields.io/docker/cloud/build/marcelohmariano/golang)](https://hub.docker.com/r/marcelohmariano/golang/builds)

A Docker container to develop with Golang.

## Getting Started

These instructions will cover usage information for the Docker container.

### Prerequisities

In order to run this container you'll need [Docker](https://docs.docker.com/get-started/) installed.

### Installation

Pull the image from the Docker repository:

```sh
docker pull marcelohmariano/golang
docker tag marcelohmariano/golang golang
docker rmi marcelohmariano/golang
```

Or build the image from source:

```sh
git clone https://github.com/marcelohmariano/golang.git
cd golang
docker build -t golang .
```

### Usage

#### Run

Build a simple Go program:

```sh
cd /path/to/your/app.go
docker run -it --rm -v $PWD:/app -w /app golang go build app.go
```

#### Volumes

* `/home/dev/go` - user packages location

#### Useful File Locations

* `/usr/local/go` - global packages location

## Built With

* [gopls](https://github.com/golang/tools/tree/master/gopls) - the official [language server](https://langserver.org/) for the Go language
* [Delve](https://github.com/go-delve/delve) - a debugger for the Go programming language.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
