FROM ubuntu:14.04

ENV DEBIAN_FRONTEND=noninteractive

# Install dependencies
RUN apt-get update && apt-get install -y \
    build-essential \
    openjdk-6-jdk \
    autoconf \
    make \
    zip \
    unzip \
    libx11-dev \
    libxext-dev \
    libxrender-dev \
    libxtst-dev \
    libxt-dev \
    libcups2-dev \
    libasound2-dev \
    libfreetype6-dev \
    libxrandr-dev \
    libgtk2.0-dev \
    git \
    ca-certificates \
    wget \
    ccache && \
    rm -rf /var/lib/apt/lists/*

# Set env variables for building JDK 7
ENV LANG=C
ENV ALT_BOOTDIR=/usr/lib/jvm/java-6-openjdk-amd64
ENV HOTSPOT_BUILD_JOBS=4
ENV SKIP_COMPARE_IMAGES=true
ENV SKIP_BOOT_CYCLE=true
ENV OUTPUTDIR=/build/output

# Clone OpenJDK 7 GA source from GitHub
WORKDIR /build
RUN git clone --branch jdk7-b147 --depth 1 https://github.com/openjdk/jdk.git jdk7

WORKDIR /build/jdk7

# Build
RUN bash ./configure \
    --with-boot-jdk=$ALT_BOOTDIR \
    --with-debug-level=release && \
    make images

# Default shell
CMD ["/bin/bash"]
