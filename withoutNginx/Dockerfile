FROM ubuntu
MAINTAINER yangwugui <yangwugui@126.com>
ENV REFRESHED_AT 2017-08-23

RUN apt-get update
RUN apt-get install -y make
RUN apt-get install -y libc6
RUN apt-get install -y libc6-dev
RUN apt-get install -y g++
RUN apt-get install -y build-essential
RUN apt-get install unzip
RUN apt-get -y install libpcre3 libpcre3-dev
RUN apt-get -y install ruby zlib1g zlib1g.dev

RUN mkdir -p /home/fastdfs
RUN mkdir -p /home/fastdfs_file/data
RUN mkdir -p /home/client
RUN ln -s /home/fastdfs_file/data /home/fastdfs_file/data/M00

WORKDIR /home/fastdfs
ADD file/fastdfs-5.08.tar.gz /home/fastdfs
ADD file/libfastcommon-master.zip /home/fastdfs/
RUN unzip libfastcommon-master.zip

WORKDIR /home/fastdfs/libfastcommon-master
RUN ./make.sh
RUN ./make.sh install

WORKDIR /home/fastdfs/fastdfs-5.08
RUN ./make.sh
RUN ./make.sh install

WORKDIR /etc/ld.so.conf.d/
RUN touch libfastcommon.conf
RUN echo "/usr/lib64/" >> libfastcommon.conf
RUN /sbin/ldconfig -v
RUN cp /home/fastdfs/fastdfs-5.08/conf/http.conf /etc/fdfs/
RUN cp /home/fastdfs/fastdfs-5.08/conf/mime.types /etc/fdfs/

WORKDIR /home/fastdfs/fastdfs-5.08
