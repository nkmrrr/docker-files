FROM ubuntu:14.04
ENV TERM linux
RUN apt-get update && apt-get -y upgrade && apt-get update

##Install SIPP
#Install tools for Compiling/building
RUN apt-get -y install build-essential git python wget
#SIPP 3.3
#Install Required Dependencies
RUN apt-get -y install autoconf libncurses5-dev libsctp-dev libpcap0.8-dev

#Install SIPP
RUN cd /usr/local/src && wget http://sourceforge.net/projects/sipp/files/sipp/3.3/sipp-3.3.tar.gz -O - | tar zxvf -
RUN cd /usr/local/src/sipp-3.3 && autoreconf -ivf && ./configure --with-pcap --with-sctp && make

ADD uac_pcap.xml /usr/local/src/sipp-3.3/
ADD auth.xml /usr/local/src/sipp-3.3/
ADD uas_pcap.xml /usr/local/src/sipp-3.3/
ADD sinfonietta.pcap /usr/local/src/sipp-3.3/pcap/sinfonietta.pcap

