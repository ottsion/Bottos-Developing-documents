# Build development environment



## Go language environment installation

Note : This machine adopts [Ubuntu Server 18.04.1 LTS](https://www.ubuntu.com/download/server) version. 

- Download go source code

```
wget https://dl.google.com/go/go1.11.linux-amd64.tar.gz
```

- Unzip go to `/usr/local` directory

```
sudo tar -zxvf go1.11.linux-amd64.tar.gz -C /usr/local
```

- Add `/usr/local/go/bin` directory to PATH environment variable

```
export PATH=$PATH:/usr/local/go/bin
```

- Check whether the Go language environment is installed successfully.

```
go env
```

If the following result is shown, the configuration is successful.

```
GOARCH="amd64"
GOBIN="/home/bottos/go/bin"
GOCACHE="/home/bottos/.cache/go-build"
GOEXE=""
GOFLAGS=""
GOHOSTARCH="amd64"
GOHOSTOS="linux"
GOOS="linux"
GOPATH="/home/bottos/go"
GOPROXY=""
GORACE=""
GOROOT="/usr/lib/go1.10"
GOTMPDIR=""
GOTOOLDIR="/usr/lib/go1.10/pkg/tool/linux_amd64"
GCCGO="gccgo"
CC="gcc"
CXX="g++"
CGO_ENABLED="1"
GOMOD=""
CGO_CFLAGS="-g -O2"
CGO_CPPFLAGS=""
CGO_CXXFLAGS="-g -O2"
CGO_FFLAGS="-g -O2"
CGO_LDFLAGS="-g -O2"
PKG_CONFIG="pkg-config"
GOGCCFLAGS="-fPIC -m64 -pthread -fmessage-length=0 -fdebug-prefix-map=/tmp/go-build892316758=/tmp/go-build -gno-record-gcc-switches"
```

- Configuring `GOPATH` working directory

Enter the directory corresponding to `GOPATH` in the return result of the above go Env, and create the corresponding working directory.



Note: the specific catalogues here are based on the actual circumstances of the individual.

```
mkdir /home/bottos/go
cd /home/bottos/go
mkdir bin pkg src src/github.com src/golang.org
```

So far, the Go environment has been built successfully.