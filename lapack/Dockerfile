FROM ogrisel/openblas

# would have been from google/golang, but openblas turned out to be
# too complicated for me to figure out.  Instead, I'll copy the
# Dockerfile from google/golang.
# Otherwise the biggest difference is that google/golang uses debian
# and openblas uses ubuntu.

# Go, taken from 
# https://registry.hub.docker.com/u/google/golang/dockerfile/
# except that I've added the libblas-dev package as well, to get 
# cblas.
RUN apt-get update -y && apt-get install --no-install-recommends -y -q curl build-essential ca-certificates git mercurial bzr libblas-dev
RUN mkdir /goroot && curl https://storage.googleapis.com/golang/go1.3.1.linux-amd64.tar.gz | tar xvzf - -C /goroot --strip-components=1
RUN mkdir /gopath

ENV GOROOT /goroot
ENV GOPATH /gopath
ENV PATH $PATH:$GOROOT/bin:$GOPATH/bin

# gonum's lapack
RUN go get github.com/gonum/lapack
RUN cd /gopath/src/github.com/gonum/lapack/clapack/ && perl genLapack.pl -L/opt/OpenBLAS/lib -lopenblas
