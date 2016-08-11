FROM    alpine:3.4

ENV     VERSION 3.1.0

RUN     mkdir -p /opt/src
COPY    src/opencv /opt/src/opencv
RUN     echo "http://dl-cdn.alpinelinux.org/alpine/edge/testing" >> /etc/apk/repositories
RUN     apk --no-cache add --virtual .buildbase \
            build-base \
            linux-headers \
        #     python \
            python-dev \
            cmake \
            libtbb \
            libtbb-dev \
            libjpeg  \
            libjpeg-turbo-dev \
            libpng-dev \
            libjasper \
            tiff-dev \
            libwebp-dev \
            py-numpy-dev \
            # py-scipy-dev \
            # gsl \
            # libavc1394-dev \
            # libdc1394-dev \
            ffmpeg-dev && \
        cd /opt/src/opencv && \
        cmake \
            -D CMAKE_BUILD_TYPE=RELEASE \
            -D CMAKE_INSTALL_PREFIX=/usr/local \
            . && \
        make VERBOSE=1 && \
        make && \
        make install && \
        rm -rf /opt && \
        apk --no-cache add --.virtual .rundeps \
            libjpeg \
            libjpeg-turbo \
            libpng \
            tiff \
            libwebp \
            libtbb
            libjasper && \
        apk del .builddeps
