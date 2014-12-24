## Anonymous GridFTP server DTN docker container

This docker container run a Globus GridFTP server in anonymous read-only access mode,
and runs the perfSONAR bwctl and owamp tools.

Data is assumed to be in /home/data. Change the path in 'docker run' if that is not the case.

build the container (in the directory containing 'Dockerfile')
>docker build -t dtn .

Run the container
>docker run -d -P --net=host -v /var/run -v /home/data:/data dtn

## Testing
test GridFTP from another host with 'globus-data-management-client' installed
>globus-url-copy -list ftp://hostname:2811/data/

>globus-url-copy -vb -fast -p 4 ftp://hostname:2811/data/test-file1 file:///dev/null

test perfSONAR tools from another host with owamp and bwctl installed:
>owping hostname

>bwctl -T iperf3 -c hostname

##Notes:

The hostname is assume to be the same is the base host. That can be changed.
See: https://docs.docker.com/articles/networking/

## Security:
make sure the following ports are allowed by the base host:
GridFTP:2811, 50000-51000  ; bwctl:4823, 5001-5900, 6001-6200 ; owamp:861, 8760-9960

###other useful docker commands 
>docker ps -a   # show running docker images and their container ID

>docker exec -it ID bash  # attach to running container

>docker stop ID

>docker rm $(docker ps -a -q ) # remove all old containers

>docker images  # list all images


