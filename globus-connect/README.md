## Anonymous GridFTP server /Globus Connect container

NOTE: this is a work in progress. Dont expect this to work yet!!

This docker container run an anonymous Globus GridFTP server configured to work with Globus Online.

Data is assumed to be in /home/data. Change the path in 'docker run' if that is not the case.

build the container (in the directory containing 'Dockerfile')
>docker build -t globus-connect .

Run the container
>docker run -d -P --net=host -v /var/run -v /home/data:/data globus-connect

## Testing

Log into http://www.globus.org, click on 'transfer files' under 'Quick Links', and type
in your username. You should see your hostname. Click on that to see what files are available for download.

You can also verify that the GridFTP server is available from the command line.
From another host with 'globus-data-management-client' installed, try this:
>globus-url-copy -list ftp://hostname:2811/data/

>globus-url-copy -vb -fast -p 4 ftp://hostname:2811/data/test-file1 file:///dev/null

##Notes:

The hostname is assumed to be the same is the base host. That can be changed.
See: https://docs.docker.com/articles/networking/

## Security:
make sure the following ports are allowed by the base host:
GridFTP:2811, 50000-51000  ; bwctl:4823, 5001-5900, 6001-6200 ; owamp:861, 8760-9960

## To Do:
Create a modified version of this container that will work with various other authentication methods.
See: https://support.globus.org/entries/24005071

