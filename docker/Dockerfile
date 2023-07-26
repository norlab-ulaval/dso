FROM ubuntu:18.04

ENV DEBIAN_FRONTEND noninteractive

RUN apt -y update \
	&& apt -y install apt-utils \
	&& apt -y install build-essential \
	&& apt -y install git \
	&& apt -y install libsuitesparse-dev libeigen3-dev libboost-all-dev \
	&& apt -y install libopencv-dev \
	&& apt -y install cmake \
	&& apt -y install libglew-dev \
	&& apt -y install libegl1-mesa-dev \
	&& apt -y install ffmpeg libavcodec-dev libavutil-dev libavformat-dev libswscale-dev libavdevice-dev \
	&& apt -y install zlib1g-dev \
	&& apt -y install sudo

# add user
# RUN adduser user sudo
RUN useradd -m user -s /bin/bash && yes password | passwd user

# create useful folders
RUN cd /home/user/ \
	&& mkdir -p repos/ \
	&& mkdir -p data

# Nedd to build Pangolin

# RUN cd /home/user/repos/ \
# 	&& git clone --recursive https://github.com/stevenlovegrove/Pangolin.git \
# 	&& cd Pangolin/ \
# 	&& git checkout v0.6 \
# 	&& mkdir build && cd build \
# 	&& cmake -DCPP11_NO_BOOST=1 .. \
# 	&& make -j4

# Nedd to build third party when in container

# Install Pylon Basler
ENV DIR=/home/user/repos/thirdparty/
RUN echo $DIR
           
RUN mkdir -p ${DIR} && \
          chmod +r ${DIR}

COPY thirdparty/ ${DIR}
RUN ls ${DIR}          
VOLUME [${DIR}]

WORKDIR ${DIR}
RUN apt -y install zlib1g-dev \
	&& apt -y install tar
RUN cd libzip-1.1.1/ \
	&& ./configure \
	&& make \
	&& make install \
	&& cp lib/zipconf.h /usr/local/include/zipconf.h

# Create user at the end to stay root for all the installation steps
USER user
WORKDIR /home/user/

