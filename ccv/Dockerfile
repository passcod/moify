FROM ubuntu:15.10
MAINTAINER Félix Saparelli <me@passcod.name>
CMD ["ccv"]

RUN apt update && DEBIAN_FRONTEND=noninteractive apt upgrade -y &&\
    DEBIAN_FRONTEND=noninteractive apt install -y \
      build-essential git wget libdispatch-dev libev-dev \
      libjpeg-dev libpng-dev libfftw3-dev libavcodec-dev \
      libavformat-dev libswscale-dev liblinear-dev &&\
\
    git clone --depth=1 git://github.com/liuliu/ccv.git /source &&\
    cd /source/lib && ./configure && make -j$(nproc) &&\
    cd ../serve && make -j$(nproc) && cd .. &&\
    rm -rf .git bin doc js site test &&\
\
    DEBIAN_FRONTEND=noninteractive apt remove -y \
      build-essential git wget libdispatch-dev libev-dev \
      libjpeg-dev libpng-dev libfftw3-dev libavcodec-dev \
      libavformat-dev libswscale-dev liblinear-dev &&\
    DEBIAN_FRONTEND=noninteractive apt-get autoremove -y &&\
    apt-get clean && rm -rf /var/lib/apt &&\
\
    echo '#!/bin/sh\ncd /source/serve; ./ccv $*' > /bin/ccv &&\
    chmod +x /bin/ccv

