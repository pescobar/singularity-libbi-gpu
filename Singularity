Bootstrap: docker
From: nvidia/cuda:10.1-cudnn7-devel-ubuntu16.04

%environment
    LC_ALL=C
    export LC_ALL
    # workaround for https://stackoverflow.com/a/30663908
    CXX="g++ -std=c++11"
    export CXX
    
%post
    export LC_ALL=C
    # Update list of available packages, then upgrade them
    apt-get update
    DEBIAN_FRONTEND=noninteractive apt-get -y upgrade

    # Install Libbi dependencies
    DEBIAN_FRONTEND=noninteractive apt-get -y install \
    libblas-dev \
    liblapack-dev \
    libqrupdate-dev \
    libboost-all-dev \
    libgsl0-dev \
    libnetcdf-dev \
    autoconf \
    automake \
    wget

    # download and install LibBi
    export LIBBI_VERSION=1.4.5
    cd /usr/local/src
    wget -O libbi-${LIBBI_VERSION}.tar.gz -nc https://github.com/lawmurray/LibBi/archive/${LIBBI_VERSION}.tar.gz
    tar -xf libbi-${LIBBI_VERSION}.tar.gz
    cd /usr/local/src/LibBi-${LIBBI_VERSION}/
    # reply yes in perl. required to use cpan in non interactive session 
    export PERL_MM_USE_DEFAULT=1
    cpan .

%runscript
    /usr/local/bin/libbi "$@"

%apprun libbi
    /usr/local/bin/libbi "$@"
