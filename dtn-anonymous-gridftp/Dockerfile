# Data Transfer Node (DTN) container

# includes GridFTP and perfSONAR tools

FROM centos:centos6
MAINTAINER Brian Tierney <bltierney@es.net>

RUN yum -y update; yum clean all
RUN yum -y install traceroute lsb yum-utils net-tools ntp python-setuptools
RUN easy_install supervisor 
RUN rpm -hUv http://software.internet2.edu/rpms/el6/x86_64/main/RPMS/Internet2-repo-0.5-3.noarch.rpm
RUN yum -y install iperf3 nuttcp bwctl owamp iperf
RUN rpm -hUv http://www.globus.org/ftppub/gt6/installers/repo/globus-toolkit-repo-latest.noarch.rpm
RUN yum -y install globus-data-management-client globus-data-management-server globus-xio-udt-driver
RUN mkdir -p /var/log/supervisor 
RUN adduser gridftp
ADD supervisord.conf /etc/supervisord.conf
ADD gridftp.conf /etc/gridftp.conf

# The following ports are used:
# GridFTP:2811, 50000-51000  
# bwctl:4823, 5001-5900, 6001-6200
# owamp:861, 8760-9960
# ranges not supported, so need to use docker run -P to expose all ports

# add GridFTP data directory
VOLUME /home/data
# add pid directory
VOLUME /var/run

CMD /usr/bin/supervisord -c /etc/supervisord.conf

