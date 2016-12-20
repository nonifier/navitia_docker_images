FROM debian:7

# use UTC as localtime
RUN rm -f /etc/localtime && ln -s /usr/share/zoneinfo/Europe/Paris /etc/localtime

RUN echo "deb http://apt.canaltp.local/debian/repositories wheezy-internal main" > /etc/apt/sources.list.d/canaltp.list

RUN apt-get update && \
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
		autotools-dev \
		libicu-dev \
		libbz2-dev \
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
		vim \
		wget && \
	apt-get clean && \
	rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN wget "http://lmde-mirror.gwendallebihan.net/latest/pool/main/b/binutils/binutils_2.22-8_amd64.deb" && \
	dpkg -i binutils_2.22-8_amd64.deb && \
	rm -f binutils_2.22-8_amd64.deb

RUN mkdir custom_boost && \
	cd custom_boost && \
	wget -O boost_1_55_0.tar.bz2 http://sourceforge.net/projects/boost/files/boost/1.55.0/boost_1_55_0.tar.bz2/download && \
	tar xvjf boost_1_55_0.tar.bz2 && \
	cd boost_1_55_0/ && \
	./bootstrap.sh --prefix=/usr/local && \
	./b2 install && \
	cd / && \
	rm -rf /custom_boost

RUN echo "/usr/lib" >> /etc/ld.so.conf

RUN pip install pip virtualenv -U
# install dependancies for libc
RUN pip install ujson==1.33 numpy==1.9

# add user and group jenkins, with specific userid and groupid, never fail
RUN groupadd -g 115 jenkins; exit 0
RUN useradd -u 109 -g 115 jenkins | chpasswd; exit 0

RUN mkdir /home/jenkins
RUN chmod 755 /home/jenkins
RUN chown 109:115 /home/jenkins

CMD ["/usr/sbin/rabbitmq-server"]
