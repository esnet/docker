## Using the Anonymous GridFTP server DTN docker image

The docker images run a Globus GridFTP server in anonymous read-only access mode,
and runs the perfSONAR bwctl and owamp tools.

Data is assumed to be in /home/data. Change the path in 'docker run' if that is not the case.

build the container (in the directory containing 'Dockerfile')
>docker build -t dtn .

Run the container
>docker run -d -P --net=host --privileged -v /var/run -v /home/data:/data dtn

## Testing
test the container (from another host with 'globus-data-management-client' installed
>globus-url-copy -list ftp://hostname:2811/data/

>globus-url-copy -vb -fast -p 4 ftp://hostname:2811/data/test-file1 file:///dev/null

test perfSONAR tools from another host with owamp and bwctl installed:
>owping hostname

>bwctl -T iperf3 -c hostname

##Notes:

The hostname is assume to be the same is the base host. That can be changed.
See: https://docs.docker.com/articles/networking/

## Security:
make sure the following ports are allowed by the base host

##other useful notes for folks new to docker
>docker ps -a   # show running docker images and their container ID

>docker exec -it ID bash  # attach to running container

>docker stop ID

>docker rm $(docker ps -a -q ) # remove all old containers

>docker images  # list all images


