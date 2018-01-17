FROM ubuntu:trusty
MAINTAINER John Kelley (john@kelley.ca)


RUN apt-get update && \
    apt-get install -y \
	bison \
	build-essential \
	clang \
	flex \
	gawk \
	git \
	graphviz \
	libffi-dev \
	libreadline-dev \
	mercurial \
	pkg-config \
	python \
	python3 \
	libftdi-dev \
	tcl-dev \
	xdot \
	vim \
    && rm -rf /var/lib/apt/lists/*

RUN mkdir /var/code && \
	useradd docker -d /var/code && \
	echo "docker:docker" | chpasswd && \
	adduser docker sudo && \
	chown docker /var/code

WORKDIR /var/code
USER root
RUN export NPROCS=`grep -c ^processor /proc/cpuinfo` && \
	git clone https://github.com/cliffordwolf/icestorm.git icestorm && \
	cd icestorm && \
	make -j$NPROCS && \
	make -j$NPROCS install && \
	cd .. && \
	rm -rf icestorm

RUN export NPROCS=`grep -c ^processor /proc/cpuinfo` && \
	cd /var/code && \
	git clone https://github.com/cseed/arachne-pnr.git arachne-pnr && \
	cd arachne-pnr && \
	make -j$NPROCS && \
	make -j$NPROCS install && \
	cd .. && \
	rm -rf arachne-pnr

RUN export NPROCS=`grep -c ^processor /proc/cpuinfo` && \
	cd /var/code && \
	git clone https://github.com/YosysHQ/yosys.git yosys && \
	cd yosys && \
	make -j$NPROCS && \
	make -j$NPROCS install && \
	cd .. && \
	rm -rf yosys

