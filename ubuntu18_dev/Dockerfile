# WARNING: DEPRECATED
# WARNING: This Dockerfile only works on KISIO platforms (because of the protobuf packages dependency)

FROM ubuntu:18.04

# use UTC as localtime
RUN rm -f /etc/localtime && ln -s /usr/share/zoneinfo/Europe/Paris /etc/localtime

### RUN echo "deb http://apt.canaltp.local/ubuntu trusty-dev main" > /etc/apt/sources.list.d/canaltp.list

RUN apt update && \
	apt install -y \
		build-essential \
		g++ \
		git \
		cmake \
		libboost-all-dev \
		python-pip \
		libzmq3-dev \
		cmake \
		libboost-all-dev \
		liblog4cplus-dev \
		libgoogle-perftools-dev \
		libprotobuf-dev \
		protobuf-compiler \
		libproj-dev \
		libosmpbf-dev \
		libpqxx3-dev \
		libssl1.0-dev \
		rabbitmq-server \
		debhelper \
		virtualenvwrapper

		
		#postgresql-server-dev-all \
		## python-dev \
		## liblog4cplus-1.0-4 \
		## libgoogle-perftools4 \
		## libprotobuf9 \
		## libprotoc9 \
		## libproj0 \
		## libgeos-c1 \
		## vim && \

# RUN	apt clean && \
# 	rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Navitia depends on boost >= 1.55
#RUN mkdir custom_boost && \
#	cd custom_boost && \
#	wget -O boost_1_55_0.tar.bz2 http://sourceforge.net/projects/boost/files/boost/1.55.0/boost_1_55_0.tar.bz2/download && \
#	tar xvjf boost_1_55_0.tar.bz2 && \
#	cd boost_1_55_0/ && \
#	./bootstrap.sh --prefix=/usr/local && \
#	./b2 install && \
#	cd / && \
#	rm -rf /custom_boost

## RUN pip install pip virtualenv -U
# install dependancies for libc
## RUN pip install ujson==1.33 numpy==1.9

# WORKDIR /var/virtualenvs
# ENV WORKON_HOME=/var/virtualenvs
# RUN /bin/bash /usr/share/virtualenvwrapper/virtualenvwrapper.sh
# RUN mkvirtualenv venv
# WORKDIR /home/navitia/src


# add user and group jenkins, with specific userid and groupid, never fail
## RUN groupadd -g 115 jenkins; exit 0
## RUN useradd -u 109 -g 115 jenkins | chpasswd; exit 0

## RUN chown -R jenkins.jenkins /home/navitia
##USER jenkins

# will contain navitia's sources
WORKDIR /home/navitia/src 

WORKDIR /home/navitia

VOLUME /home/navitia/navitia_build

CMD cmake -DCMAKE_BUILD_TYPE=Release ../src/source
