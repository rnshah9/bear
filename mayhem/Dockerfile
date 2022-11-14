FROM --platform=linux/amd64 ubuntu:22.04 as builder

RUN apt-get update
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y build-essential python-is-python3 cmake pkg-config libfmt-dev libspdlog-dev nlohmann-json3-dev \
    libgrpc++-dev protobuf-compiler-grpc libssl-dev

COPY . /repo
WORKDIR /repo/build
RUN cmake .. -DCMAKE_INSTALL_PREFIX=/install
RUN make -j8
RUN make install

FROM ubuntu:22.04 as package
RUN apt-get update
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y protobuf-compiler libspdlog-dev libgrpc++-dev libfmt-dev
COPY --from=builder /install /install
