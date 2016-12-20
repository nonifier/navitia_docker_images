FROM debian:8

# use UTC as localtime
RUN rm -f /etc/localtime && ln -s /usr/share/zoneinfo/Europe/Paris /etc/localtime

RUN apt-get update &&
	apt-get install -y python-pip \
		git \
		postgresql-server-dev-all \
		python-dev \
		libzmq-dev \
		debhelper \
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

RUN pip install pip virtualenv -U
# install dependancies for libc
RUN pip install ujson==1.33 numpy==1.9

# add user and group jenkins, with specific userid and groupid, never fail
RUN groupadd -g 115 jenkins; exit 0
RUN useradd -u 109 -g 115 jenkins | chpasswd; exit 0

CMD ["/usr/sbin/rabbitmq-server"]
