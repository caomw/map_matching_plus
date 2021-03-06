FROM gyllen/mapillary_base_ubuntu:0.0.3


RUN add-apt-repository -y ppa:ubuntu-toolchain-r/test && apt-get update -y && \
    apt-get install -y \
    autoconf automake libtool make \
    gcc-4.9 g++-4.9 \
    libboost1.54-dev \
    libboost-program-options1.54-dev \
    libboost-filesystem1.54-dev \
    libboost-system1.54-dev \
    libboost-thread1.54-dev \
    protobuf-compiler \
    libprotobuf-dev \
    lua5.2 \
    liblua5.2-dev \
    git \
    libsqlite3-dev \
    libspatialite-dev \
    libgeos-dev \
    libgeos++-dev \
    libcurl4-openssl-dev \
    wget \
    lcov \
    libzmq3 libzmq3-dev \
    cmake && \
    update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-4.9 90 && \
    update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-4.9 90


RUN mkdir /source
WORKDIR /source


RUN git clone --depth=1 --recurse-submodules https://github.com/kevinkreiser/prime_server.git && \
    cd prime_server && \
    ./autogen.sh && ./configure && \
    make && make install && \
    rm -rf /source/prime_server


RUN git clone --depth=1 --recurse-submodules https://github.com/valhalla/midgard.git && \
    cd midgard && \
    ./scripts/install.sh && \
    rm -rf /source/midgard


RUN git clone --depth=1 --recurse-submodules https://github.com/valhalla/baldr.git && \
    cd baldr && \
    ./autogen.sh && ./configure CPPFLAGS=-DBOOST_SPIRIT_THREADSAFE && \
    make valhalla/baldr/date_time_zonespec.h && \
    make && make install && \
    rm -rf /source/baldr


RUN git clone --depth=1 --recurse-submodules https://github.com/valhalla/skadi.git && \
    cd skadi && \
    ./scripts/install.sh && \
    rm -rf /source/skadi


RUN git clone --depth=1 --recurse-submodules https://github.com/valhalla/mjolnir.git && \
    cd mjolnir && \
    ./scripts/install.sh && \
    rm -rf /source/mjolnir


RUN git clone --depth=1 --recurse-submodules https://github.com/valhalla/sif.git && \
    cd sif && \
    ./scripts/install.sh && \
    rm -rf /source/sif


RUN git clone --depth=1 --recurse-submodules https://github.com/miloyip/rapidjson.git && \
    cd rapidjson && \
    git submodule update --init && \
    mkdir build && cd build && \
    cmake .. && \
    make && make install && \
    rm -rf /source/rapidjson


RUN git clone --depth=1 --recurse-submodules http://github.com/mapillary/map_matching_plus.git && \
    cd map_matching_plus && \
    make service && sudo install service /usr/local/bin/mm_service && \
    rm -rf /source/map_matching_service
