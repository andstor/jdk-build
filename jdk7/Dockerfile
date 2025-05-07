FROM ubuntu:14.04

ENV DEBIAN_FRONTEND=noninteractive

# Install dependencies
RUN apt-get update && \
    apt-get install -y \
    build-essential \
    openjdk-6-jdk \
    autoconf \
    make \
    zip \
    unzip \
    gawk \
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
    ccache \
    ant && \
    rm -rf /var/lib/apt/lists/*

# Environment variables
ENV LANG=C
ENV ALT_BOOTDIR=/usr/lib/jvm/java-6-openjdk-amd64
ENV HOTSPOT_BUILD_JOBS=4
ENV SKIP_COMPARE_IMAGES=true
ENV SKIP_BOOT_CYCLE=true
ENV OUTPUTDIR=/build/output
ENV DROPS_DIR=/java/devtools/share/jdk7-drops

# Prepare build directory
WORKDIR /build

# Clone OpenJDK 7 GA source from GitHub
RUN git clone --branch jdk7-b147 --depth 1 https://github.com/openjdk/jdk.git jdk7

# Clone jaxp drop-in repo
RUN mkdir -p /java/devtools/share && \
    git clone https://github.com/openjdk-mirror/jdk7u-jaxp.git $DROPS_DIR

# Build JDK
WORKDIR /build/jdk7
RUN make sanity && \
    ant -Djdk.home=$ALT_BOOTDIR -Ddrops.dir=$DROPS_DIR -Doutput.dir=$OUTPUTDIR -f jaxp/make/build.xml all && \
    make all

# Default shell
CMD ["/bin/bash"]
