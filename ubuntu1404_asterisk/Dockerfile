FROM ubuntu:14.04
ENV TERM linux
RUN apt-get update && apt-get -y upgrade
RUN apt-get update

##Install Asterisk
#Install tools for compiling/building
RUN apt-get -y install pkg-config
RUN apt-get -y install build-essential libtool
RUN apt-get -y install autoconf automake
RUN apt-get -y install wget curl
RUN apt-get -y install git-core subversion

#Install Required Dependencies
RUN apt-get -y install openssl libssl-dev
RUN apt-get -y install libxml2-dev libncurses5-dev
RUN apt-get -y install uuid uuid-dev
RUN apt-get -y install libjansson4 libjansson-dev
RUN apt-get -y install sqlite3 libsqlite3-dev
RUN apt-get -y install speex libspeex-dev libogg-dev

#Compile and install pjproject
RUN cd /usr/local/src && wget http://www.pjsip.org/release/2.4.5/pjproject-2.4.5.tar.bz2 -O - | tar -xjvf -
RUN cd /usr/local/src/pjproject-2.4.5 && ldconfig && ./configure --prefix=/usr --enable-shared --disable-sound --disable-resample --disable-video --disable-opencore-amr CFLAGS='-O2 -DNDEBUG'
RUN cd /usr/local/src/pjproject-2.4.5 && make dep && make && make install && ldconfig

#Compile and install Asterisk
RUN cd /usr/local/src && wget http://downloads.asterisk.org/pub/telephony/asterisk/asterisk-13-current.tar.gz -O - | tar zxvf -
RUN cd /usr/local/src/asterisk-13* && ./configure
RUN cd /usr/local/src/asterisk-13* && make && make install && make config && make samples

RUN mv /etc/asterisk/pjsip.conf /etc/asterisk/pjsip.conf.sample
RUN mv /etc/asterisk/sip.conf /etc/asterisk/pjsip.conf.sample
RUN touch /etc/asterisk/sip.conf
RUN mv /etc/asterisk/extensions.conf /etc/asterisk/extensions.conf.sample

ADD pjsip.conf /etc/asterisk/
ADD extensions.conf /etc/asterisk/
