FROM ubuntu:20.04

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get clean && \
    apt-get update --fix-missing && \
    apt-get install cmake make gcc g++ flex libfl-dev bison libpcap-dev libssl-dev python3 python3-dev swig zlib1g-dev libgoogle-perftools-dev --yes --no-install-recommends && \
    apt-get clean

# 1. install zeek
COPY zeek-4.1.0.tar.gz /tmp/zeek-4.1.0.tar.gz
RUN tar xvfz /tmp/zeek-4.1.0.tar.gz --directory /tmp/ && \
    cd /tmp/zeek-4.1.0 && \
    ./configure --build-type=Release --disable-auxtools --disable-archiver --disable-python --disable-broker-tests --disable-zeekctl --enable-perftools && \
    make && \
    make install && \
    rm -rf /tmp/zeek-4.1.0 /tmp/zeek-4.1.0.tar.gz

# 2. install spicy
COPY spicy-1.2.1.tar.gz /tmp/spicy-1.2.1.tar.gz
RUN tar xvfz /tmp/spicy-1.2.1.tar.gz --directory /tmp/ && \
    cd /tmp/spicy-1.2.1 && \
    ./configure --enable-ccache && \
    make && \
    make install && \
    rm -rf /tmp/spicy-1.2.1 /tmp/spicy-1.2.1.tar.gz

# 3. install spicy-plugin
COPY spicy-plugin-1.2.3.tar.gz /tmp/spicy-plugin-1.2.3.tar.gz
RUN tar xvfz /tmp/spicy-plugin-1.2.3.tar.gz --directory /tmp/ && \
    cd /tmp/spicy-plugin-1.2.3 && \
    (mkdir build && cd build && cmake -DCMAKE_INSTALL_PREFIX=/opt/spicy .. && make -j `nproc`) && \
    make -C build install && \
    rm -rf /tmp/spicy-plugin-1.2.3 /tmp/spicy-plugin-1.2.3.tar.gz

# 4. install spicy-analyzers
COPY spicy-analyzers-0.2.23.tar.gz /tmp/spicy-analyzers-0.2.23.tar.gz
RUN tar xvfz /tmp/spicy-analyzers-0.2.23.tar.gz --directory /tmp/ && \
    cd /tmp/spicy-analyzers-0.2.23 && \
    (mkdir -p build && cd build && cmake -DCMAKE_INSTALL_PREFIX=/opt/spicy .. && make -j 1) && \
    make -C build install && \
    rm -rf /tmp/spicy-analyzers-0.2.23 /tmp/spicy-analyzers-0.2.23.tar.gz

ENV PATH $PATH:/usr/local/zeek/bin

RUN echo 'export PS1="\[\033[01;32m\][\u@\h\[\033[01;37m\] \W\[\033[01;32m\]]\[\033[00m\] "' >> /root/.bashrc
