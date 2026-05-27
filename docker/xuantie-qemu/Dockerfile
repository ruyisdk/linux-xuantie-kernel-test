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

# install xuantie cross-compilation toolchain
RUN set -x \
    && wget -qc https://occ-oss-prod.oss-cn-hangzhou.aliyuncs.com/resource//1777015432925/Xuantie-900-gcc-linux-6.6.36-glibc-x86_64-V3.4.0-20260323.tar.gz -O toolchain.tar.gz \
    && tar -xzf toolchain.tar.gz -C /opt \
    && rm toolchain.tar.gz \
    && : # last line

# install xuantie linux SDK
RUN set -x \
    && wget -qc https://occ-oss-prod.oss-cn-hangzhou.aliyuncs.com/resource//1777269751788/xuantie-linux-V1.3.0.tar.gz -O linux_sdk.tar.gz \
    && mkdir -p /opt/xuantie-linux-sdk \
    && tar -xzf linux_sdk.tar.gz -C /opt/xuantie-linux-sdk \
    && rm linux_sdk.tar.gz \
    && : # last line

# install qemu
RUN set -x \
    && wget -qc https://occ-oss-prod.oss-cn-hangzhou.aliyuncs.com/resource//1775267528397/xuantie-qemu-x86_64-Ubuntu-20.04-V5.4.1.tar.gz -O qemu_package.tar.gz \
    && mkdir -p /qemu \
    && tar -xzf qemu_package.tar.gz -C /qemu \
    && rm qemu_package.tar.gz \
    && : # last line

# Set environment variables
ENV XUANTIE_TOOLCHAIN=/opt/Xuantie-900-gcc-linux-6.6.36-glibc-x86_64-V3.4.0
ENV XUANTIE_LINUX_SDK=/opt/xuantie-linux-sdk/archived
ENV PATH=${PATH}:/qemu/bin:${XUANTIE_TOOLCHAIN}/bin

WORKDIR /root

RUN qemu-system-riscv64 -cpu help
