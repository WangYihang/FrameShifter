FROM centos:8

ARG ats_version

RUN sed -i 's/mirrorlist/#mirrorlist/g' /etc/yum.repos.d/CentOS-*
RUN sed -i 's|#baseurl=http://mirror.centos.org|baseurl=http://vault.centos.org|g' /etc/yum.repos.d/CentOS-*

RUN yum update -y
RUN yum install -y pkgconfig libtool gcc gcc-c++ make openssl openssl-devel pcre libcap flex hwloc lua zlib curl tcl-devel pcre-devel bzip2

COPY --chown=root:root ./trafficserver-${ats_version}.tar.bz2 /root/

WORKDIR /root/

RUN tar -xvf trafficserver-${ats_version}.tar.bz2

WORKDIR /root/trafficserver-${ats_version}

RUN ./configure && make && make install


EXPOSE 80
EXPOSE 443

# Copy startup script.
COPY trafficserver_startup /usr/local/bin/

# Start!
CMD ["trafficserver_startup"]
