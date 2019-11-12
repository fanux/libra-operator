FROM centos:7.6.1810
RUN yum install -y unzip make automake autoconf wget openssl-devel libtool zlib gcc-c++.x86_64 git which 
RUN wget https://github.com/Kitware/CMake/releases/download/v3.15.5/cmake-3.15.5.tar.gz \
	&& tar zxvf cmake-3.15.5.tar.gz \
	&& cd cmake-3.15.5 \
	&& ./configure && make && make install
RUN PROTOC_VERSION=3.8.0 \
    && PROTOC_ZIP=protoc-$PROTOC_VERSION-linux-x86_64.zip \
    && curl -OL https://github.com/protocolbuffers/protobuf/releases/download/v$PROTOC_VERSION/$PROTOC_ZIP \
    && unzip -o $PROTOC_ZIP -d /usr/local bin/protoc \
    && unzip -o $PROTOC_ZIP -d /usr/local include/* \
    && rm -f $PROTOC_ZIP
RUN git clone https://github.com/fanux/libra.git \
	&& cd libra && git checkout fanux-testnet \
	&& ./scripts/dev_setup.sh && ./scripts/cli/build_cli.sh
WORKDIR /libra
CMD ./target/debug/client --host ac.testnet.libra.org --port 8000 -s ./scripts/cli/consensus_peers.config.toml
