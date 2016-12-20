# WARNING: DEPRECATED
# WARNING: This Dockerfile only works on KISIO platforms (because of the protobuf packages dependency)

FROM ubuntu:14.04

# use UTC as localtime
RUN rm -f /etc/localtime && ln -s /usr/share/zoneinfo/Europe/Paris /etc/localtime

RUN echo "deb http://apt.canaltp.local/ubuntu trusty-dev main" > /etc/apt/sources.list.d/canaltp.list

RUN apt-get update && \
	apt-get install -y python-pip \
		git \
		postgresql-server-dev-all \
		python-dev \
		libzmq-dev debhelper \
		build-essential \
		cmake \
		gcc \
		g++ \
		libboost-all-dev \
		liblog4cplus-1.0-4 \
		liblog4cplus-dev \
		libgoogle-perftools4 \
		libgoogle-perftools-dev && \
	apt-get install -y --force-yes libprotobuf9 \
		libprotobuf-dev \
		libprotoc9 \
		protobuf-compiler \
		libproj0 \
		libproj-dev \
		libosmpbf-dev \
		libpqxx3-dev \
		rabbitmq-server \
		libgeos-c1 \
		vim && \
	apt-get clean && \
	rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Navitia depends on boost >= 1.55
RUN mkdir custom_boost && \
	cd custom_boost && \
	wget -O boost_1_55_0.tar.bz2 http://sourceforge.net/projects/boost/files/boost/1.55.0/boost_1_55_0.tar.bz2/download && \
	tar xvjf boost_1_55_0.tar.bz2 && \
	cd boost_1_55_0/ && \
	./bootstrap.sh --prefix=/usr/local && \
	./b2 install && \
	cd / && \
	rm -rf /custom_boost

RUN pip install pip virtualenv -U
# install dependancies for libc
RUN pip install ujson==1.33 numpy==1.9

# add user and group jenkins, with specific userid and groupid, never fail
RUN groupadd -g 115 jenkins; exit 0
RUN useradd -u 109 -g 115 jenkins | chpasswd; exit 0

CMD ["/usr/sbin/rabbitmq-server"]
