# Pull base image
FROM ubuntu:20.04

# Install tools by apt
# Install tools by apt
ENV DEBIAN_FRONTEND=noninteractive
RUN set -x \
    && apt-get -y update \
    && apt-get -y install \
# essential tools
    apt-utils \
    git \
    wget \
    vim \
    gawk \
    flex \
    bison \
    gperf \
    telnet \
    bc \
    curl \
    zip \
    unzip \
    z3 \
    texinfo \
    sudo \
    expect \
    cpio \
    rsync \
# python3
    python3 \
    python3-pip \
# network tools
    iputils-ping \
    net-tools \
# building tools
    build-essential \
    make \
    autoconf \
    automake \
    autotools-dev \
    gcc \
    g++ \
    pkg-config \
    libtool \
    device-tree-compiler \
    patchutils \
# gdb dependencies
    libncurses* \
    libncurses5-dev \
# qemu dependencies
    libnuma-dev \
    libcurl4-gnutls-dev \
    libiscsi-dev \
    libaio-dev \
    libnfs-dev \
    librbd-dev \
    libxkbcommon-dev \
    libfdt-dev \
    libpixman-1-dev \
    libepoxy-dev \
    libpng-dev \ 
    libjpeg-turbo8-dev \
    libsnappy-dev \
    liblzo2-dev \
    libsdl2-dev \
    libvdeplug-dev \
    libgtk-3-dev \
    libcacard-dev \
    libbrlapi-dev \
    libcapstone-dev \
    libspice-server-dev \ 
    libpmem-dev \
    libdaxctl-dev \
    libslirp-dev \
    libsdl2-image-dev \
    libvirglrenderer-dev \
    libusbredirhost-dev \
    libfuse3-dev \
    && apt clean && rm -rf /var/lib/apt/lists \
    && update-alternatives --install /usr/bin/python python /usr/bin/python3 1 \
    && : # last line

# install packages via pip3
RUN set -x \
    && python3 -m pip install -U pip setuptools \
    && pip3 install -U \
        pexpect \
        PyYAML \
        pyserial \
        requests \
        numpy \
        pytest \
        pytest-html \
        pytest-timeout \
        pytest-repeat \
        pytest-logbook \
        pytest-rerunfailures \
        pytest-xdist \
        pytest-ordering \
        pytest-assume \
        allure-pytest \
        prettytable \
        colorlog \
    && : # last line

# install qemu
RUN set -x \
    && wget -qc http://yocbook.oss-cn-hangzhou.aliyuncs.com/depot/qemu/Xuantie-qemu-x86_64-Ubuntu-20.04-V4.2.9-B20240416-0338.tar.gz -O qemu_package.tar.gz\
    && tar -xzf qemu_package.tar.gz \
    && rm qemu_package.tar.gz \
    && mv install qemu \
    && : # last line


# Set environment variables

ENV PATH=${PATH}:/qemu/bin

WORKDIR /root

RUN qemu-system-riscv64 -cpu help
