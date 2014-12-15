# Data Transfer Node (DTN) container

# includes GridFTP and perfSONAR tools

FROM centos:centos6
MAINTAINER Brian Tierney <bltierney@es.net>
# Quagga config from: https://github.com/fredhsu/docker-quagga

RUN yum -y update; yum clean all
#RUN yum -i groupinstall "Development Tools"
RUN yum -y install traceroute lsb yum-utils net-tools ntp quagga python-setuptools
RUN easy_install supervisor 
RUN rpm -hUv http://software.internet2.edu/rpms/el6/x86_64/main/RPMS/Internet2-repo-0.5-3.noarch.rpm
RUN yum -y install iperf3 nuttcp bwctl owamp iperf
RUN rpm -hUv http://www.globus.org/ftppub/gt6/installers/repo/globus-toolkit-repo-latest.noarch.rpm
RUN yum -y install globus-data-management-client globus-data-management-server globus-xio-udt-driver
RUN mkdir -p /var/log/supervisor 
RUN adduser gridftp
# if want to try to add sshftp support (note: this will require getting sshd to work too)
#RUN /etc/init.d/globus-gridftp-sshftp start
# fix for GT6.0 bug
#RUN sed 's/@SSH_BIN@/\/usr\/bin\/ssh/' -i /usr/share/globus/gridftp-ssh
ADD supervisord.conf /etc/supervisord.conf
ADD gridftp.conf /etc/gridftp.conf

# enable quagga daemons
#RUN sed -i 's/=no/=yes/g' /etc/quagga/daemons
# turn on ip forwarding
#RUN echo "1" > /proc/sys/net/ipv4/ip_forward
#RUN cp /usr/share/doc/quagga/examples/*.sample /etc/quagga/
#RUN echo "for curFile in /etc/quagga/*.sample; do mv \"\$curFile\" \"\${curFile:0:-7}\"; done" | bash

# The following ports are used:
# GridFTP:2811, 50000-51000  
# bwctl:4823, 5001-5900, 6001-6200
# owamp:861, 8760-9960
# bgp: 179
# quagga mgmt ports 2601 2602 2603 2604 2605 2606

# ranges not supported, so need to use docker run -P to expose all ports
#EXPOSE 179 861 2601-1606 2811 4823 5001-5900 6001-6200 8760-9960 50000-51000

# add GridFTP data directory
VOLUME /home/data
# add pid directory
VOLUME /var/run

#CMD ["/usr/bin/supervisord","-c /etc/supervisord.conf"]
CMD /usr/bin/supervisord -c /etc/supervisord.conf

