## GridFTP server /Globus Connect container

NOTE: this is a work in progress. Dont expect this to work yet!!

This docker container run a Globus GridFTP server configured to work with Globus Online

Data is assumed to be in /home/data. Change the path in 'docker run' if that is not the case.

build the container (in the directory containing 'Dockerfile')
>docker build -t globus-connect .

Run the container
>docker run -d -P --net=host -v /var/run -v /home/data:/data globus-connect

Attach to the running container, and run 'globus-connect-server-setup'
>docker ps -a # get the container ID
>docker exec -it ID bash # attach to running container
>globus-connect-server-setup   #enter globus username/password
>exit  # exit running container
># commit changes made by globus-connect-server-setup script
>docker commit -m "configured globus connect server" ID globus-connect  




## Testing
test GridFTP from another host with 'globus-data-management-client' installed
>globus-url-copy -list ftp://hostname:2811/data/

>globus-url-copy -vb -fast -p 4 ftp://hostname:2811/data/test-file1 file:///dev/null

##Notes:

The hostname is assume to be the same is the base host. That can be changed.
See: https://docs.docker.com/articles/networking/

## Security:
make sure the following ports are allowed by the base host:
GridFTP:2811, 50000-51000  ; bwctl:4823, 5001-5900, 6001-6200 ; owamp:861, 8760-9960


