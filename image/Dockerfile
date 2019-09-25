FROM debian:buster
ENV DEBIAN_FRONTEND=noninteractive
COPY docker-apt-minify /etc/dpkg/dpkg.cfg.d/
RUN apt-get -y update && \
    apt-get -y install \
        autoconf \
        g++ \
        libboost-filesystem-dev \
        libboost-iostreams-dev \
        libboost-program-options-dev \
        libboost-serialization-dev \
        libboost-system-dev \
        libboost-thread-dev \
        libbz2-dev \
        libtool \
        make \
        unzip \
        wget \
        zlib1g-dev && \
    rm -r /var/lib/apt/lists/*
ARG commitid=0df53bb6e3d79410e8501502c365d8200153477e
RUN cd /usr/src && \
    wget https://github.com/cr-marcstevens/hashclash/archive/$commitid.zip && \
    unzip $commitid.zip && \
    mv hashclash-$commitid hashclash
RUN cd /usr/src/hashclash && \
    autoreconf -i && \
    ./configure && \
    make -j$(getconf _NPROCESSORS_ONLN) && \
    find . \
        \( \
            -name "*.o" -o \
            -name "*.lo" -o \
            -name "*.Po" -o \
            -name "*.Plo" \
        \) -delete
