# gRPC Example

- Golang Server
- PHP Client

## Folder Structure

- `./service.proto` - service definition, used for compiling protobuf files
- `./server/main.go` - simple golang greeter service
- `./client/greeter_client.php` - php client that calls greeter service
- `./client/composer.json` - composes php client

## Usage

In this example we will use [docker](https://docs.docker.com/engine/installation/)
to run a Centos 7 virtual machine. We will install all necessary software inside this VM.

### Clone repo

You will need to mount the code in this repo into the VM we are about to setup.
So first clone this repo...

```
$ git clone https://github.com/smaxwellstewart/grpc-go-php
```

### Setup Centos 7 VM

```
$ docker pull centos:7
$ docker run -i -t -v `pwd`/grpc-go-php:/gohome/src/github.com/smaxwellstewart/grpc-go-php centos:7
```

Now you will be inside the Centos 7 virtual machine. All commands below will be
run inside of this VM.

### Install `protoc`

```
$ yum install autoconf automake libtool unzip gcc-c++ git wget make -y
$ wget https://github.com/google/protobuf/archive/v3.4.1.zip
$ unzip v3.4.1.zip
$ cd protobuf-3.4.1
$ ./autogen.sh
$ ./configure
$ make
$ mv src/protoc /bin/protoc
```


### Setup `go` enviroment

First install go and required libs...

```
$ yum install golang
$ export GOPATH=/gohome
$ go version
$ go get google.golang.org/grpc
$ go get -u github.com/golang/protobuf/protoc-gen-go
$ export PATH=$PATH:$GOPATH/bin
```

### Compile protobuf code for server

```
cd /grpc-go-php
```


### Install `go` greeter service

### Generate PHP Client

```
$ GRPC_PHP_PLUGIN_PATH=/{yourpath}/bins/opt/grpc_php_plugin
$ protoc --proto_path=. \
  --php_out=client/lib \
  --grpc_out=client/lib \
  --plugin=protoc-gen-grpc=$GRPC_PHP_PLUGIN_PATH \
  ./service.proto
```
