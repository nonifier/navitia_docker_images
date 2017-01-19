FROM alpine:edge

RUN echo http://dl-3.alpinelinux.org/alpine/edge/testing  >> /etc/apk/repositories
WORKDIR /
RUN apk --update --no-cache add \
    g++ \
    build-base \
    python \
    musl-dev \
    linux-headers \
    python-dev \
    py2-pip \
    git \
    curl \
    automake \
    autoconf \
    libtool && \
    pip install  --no-cache-dir -U pip && \
    pip install --no-cache-dir uwsgi && \
    git clone https://github.com/google/protobuf.git && cd protobuf && \
    git checkout v3.1.0 && ./autogen.sh && ./configure && make -j$(grep -c vendor_id /proc/cpuinfo) && \
    make install && \
    cd python && python setup.py install --cpp_implementation && \
    cd / && rm -rf protobuf && apk del \
        g++ \
        build-base \
        python-dev \
        git \
        curl \
        automake \
        autoconf \
        libtool \
        musl-dev \
        linux-headers
