FROM ubuntu:20.04
RUN apt-get update
ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get install -y wget build-essential libssl-dev git cmake
ENV MY_INSTALL_DIR=$HOME/.local
RUN mkdir -p $MY_INSTALL_DIR
RUN git clone --recurse-submodules -b v1.46.3 --depth 1 --shallow-submodules https://github.com/grpc/grpc /grpc
WORKDIR /grpc
RUN git submodule update --
RUN mkdir -p cmake/build
WORKDIR ./cmake/build
RUN apt-get install -y protobuf-compiler
RUN cmake -DgRPC_INSTALL=ON -DgRPC_BUILD_TESTS=OFF -DCMAKE_INSTALL_PREFIX=$MY_INSTALL_DIR ../..
RUN make -j6
RUN make install
WORKDIR /grpc/examples/cpp/helloworld
RUN mkdir -p cmake/build
WORKDIR /grpc/examples/cpp/helloworld/cmake/build
RUN cmake -DCMAKE_PREFIX_PATH=$MY_INSTALL_DIR ../..
RUN make -j6