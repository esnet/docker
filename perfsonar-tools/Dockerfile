# perfSONAR tools

FROM centos:centos7
MAINTAINER Brian Tierney <bltierney@es.net>

RUN yum -y install epel-release
RUN yum -y update; yum clean all
RUN rpm -hUv http://software.internet2.edu/rpms/el6/x86_64/main/RPMS/Internet2-repo-0.6-1.noarch.rpm
RUN yum -y install perfsonar-tools
RUN yum -y install supervisor net-tools systat tcsh tcpdump # grab a few other favorite tools

RUN mkdir -p /var/log/supervisor 
ADD supervisord.conf /etc/supervisord.conf

# The following ports are used:
# bwctl:4823, 5001-5900, 6001-6200
# owamp:861, 8760-9960
# ranges not supported, so need to use docker run -P to expose all ports

# add pid directory
VOLUME /var/run

CMD /usr/bin/supervisord -c /etc/supervisord.conf

