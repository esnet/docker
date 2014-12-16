## perfSONAR Light docker container

The docker container runs all perfSONAR light services.
See: https://code.google.com/p/perfsonar-ps/wiki/Level1and2Install 

build the container (in the directory containing 'Dockerfile')
>docker build -t ps_light .

Run the container
>docker run -d -P --net=host -v /var/run ps_light

## Testing

test perfSONAR tools from another host with owamp and bwctl installed:
>owping hostname

>bwctl -T iperf3 -c hostname

##Notes:

The hostname is assume to be the same is the base host. That can be changed.
See: https://docs.docker.com/articles/networking/

## Security:
make sure the following ports are allowed by the base host:
 bwctl:4823, 5001-5900, 6001-6200 ; owamp:861, 8760-9960, lookup service: 8090, 8096
See: http://www.perfsonar.net/deploy/security-considerations/


###other useful docker commands 
>docker ps -a   # show running docker images and their container ID

>docker exec -it ID bash  # attach to running container

>docker stop ID

>docker rm $(docker ps -a -q ) # remove all old containers

>docker images  # list all images


