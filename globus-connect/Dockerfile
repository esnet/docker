# Globus Connect/GridFTP container
# https://www.globus.org/globus-connect-server

# includes GridFTP and Globus Connect
# also includes some network test tools

FROM centos:centos6
MAINTAINER Brian Tierney <bltierney@es.net>

RUN yum -y update; yum clean all
RUN yum -y install traceroute lsb yum-utils net-tools python-setuptools
RUN easy_install supervisor 
RUN rpm -hUv http://software.internet2.edu/rpms/el6/x86_64/main/RPMS/Internet2-repo-0.5-3.noarch.rpm
RUN yum -y install iperf3 nuttcp bwctl owamp iperf
RUN rpm -hUv http://www.globus.org/ftppub/gt6/installers/repo/globus-toolkit-repo-latest.noarch.rpm
RUN yum -y install globus-data-management-client globus-data-management-server globus-xio-udt-driver
RUN yum -y install globus-connect-server
RUN mkdir -p /var/log/supervisor 
RUN adduser gridftp
ADD supervisord.conf /etc/supervisord.conf
ADD gridftp.conf /etc/gridftp.conf
ADD globus-connect-server.conf /etc/globus-connect-server.conf
# globus-connect-server-setup script needs these
ENV HOME /root
ENV TERM xterm

# The following ports are used:
# GridFTP:2811, 50000-51000  
# ranges not supported, so need to use docker run -P to expose all ports

# add GridFTP data directory
VOLUME /home/data
# add pid directory
VOLUME /var/run

CMD /usr/bin/supervisord -c /etc/supervisord.conf

