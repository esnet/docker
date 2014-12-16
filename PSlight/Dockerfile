# perfSONAR Light

FROM centos:centos6
MAINTAINER Brian Tierney <bltierney@es.net>

RUN yum -y update; yum clean all
RUN yum -y install traceroute net-tools ntp python-setuptools
RUN easy_install supervisor 
RUN rpm -hUv https://dl.fedoraproject.org/pub/epel/6/x86_64/epel-release-6-8.noarch.rpm
RUN rpm -hUv http://software.internet2.edu/rpms/el6/x86_64/main/RPMS/Internet2-repo-0.5-3.noarch.rpm
RUN yum -y install perfSONAR_PS-Bundles-Level1
RUN mkdir -p /var/log/supervisor 
ADD supervisord.conf /etc/supervisord.conf

# The following ports are used:
# bwctl:4823, 5001-5900, 6001-6200
# owamp:861, 8760-9960
# ranges not supported, so need to use docker run -P to expose all ports

# add pid directory
VOLUME /var/run

CMD /usr/bin/supervisord -c /etc/supervisord.conf
