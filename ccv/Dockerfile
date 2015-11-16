FROM alpine
MAINTAINER Félix Saparelli <me@passcod.name>
CMD ["ccv"]

RUN apk add --update build-base autoconf automake git libev libev-dev \
      libpng libpng-dev libjpeg libjpeg-turbo libjpeg-turbo-dev fftw \
      fftw-dev ffmpeg ffmpeg-dev ffmpeg-libs && rm -rf /var/cache/apk/*

RUN apk add --update libtool bsd-compat-headers linux-headers

RUN git clone git://github.com/mheily/libkqueue.git /kq
RUN cd /kq && git checkout tags/REL_2_0_1 && ./configure && make && make install

RUN git clone --depth=1 git://git.macosforge.org/libdispatch.git /dispatch
RUN cd /dispatch && sh autogen.sh && ./configure && make && make install

RUN git clone --depth=1 git://github.com/liuliu/ccv.git /source
RUN cd /source/lib && ./configure && make
RUN cd /source && make install

RUN cd /source/serve && make
RUN apk del libev-dev libpng-dev libjpeg-turbo-dev fftw-dev ffmpeg-dev \
      build-base git autoconf automake libtool bsd-compat-headers linux-headers

