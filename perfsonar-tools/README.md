## perfSONAR Tools docker container

The docker container runs all perfSONAR tools in the "Tools" bundle, as described at:
http://docs.perfsonar.net/install_options.html

This can be used to run perfSONAR Tools on any OS that supports docker.

Download the container:
>docker pull bltierney/perfsonar-tools

Run the container:
>docker run -d -P --net=host -v /var/run bltierney/perfsonar-tools

## Testing

test perfSONAR tools from another host with owamp and bwctl installed:
>owping hostname

>bwctl -T iperf3 -c hostname

##Notes:
The perfSONAR hostname is assume to be the same is the base host. To use a different
name/IP for the perfSONAR container, see: https://docs.docker.com/articles/networking/

## Security:
make sure the following ports are allowed by the base host:
 pScheduler: 443, bwctl:4823, 5001-5900, 6001-6200 ; owamp:861, 8760-9960
See: http://www.perfsonar.net/deploy/security-considerations/



