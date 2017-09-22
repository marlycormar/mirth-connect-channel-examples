# MIRTH CONNECT DOCKER IMAGE

There are basically two ways to create a container from this image:

----------------------------------------------------------

### I.A Create default container from image
        docker run -d -P --name mirth marlycormar/mirth-connect-3.5.1

----------------------------------------------------------

### I.B Create container from image with customized Mirth Connect server configuration
1. Download configuration file from: `https://github.com/marlycormar/mirth-connect-3.5.1/blob/master/mirth.properties.example`

1. Rename the file to `mirth.properties`:
        mv mirth.properties.example mirth.properties 

1. Make the necessary changes to the file, e.g., add db credentials.

1. Run Mirth Connect with this configuration:
        
        docker run -d -P -v <absolute_path>/mirth.properties:/opt/mirth-connect/conf/mirth.properties marlycormar/mirth-connect-3.5.1

----------------------------------------------------------

### II. Open Mirth Connect
After the container has been created, followed the steps below to open Mirth Connect.

### Mirth Connect container using previously created image

1. Check the ports on which the server is running:
        docker ps

1. Download mirth connect admin by going to:
        127.0.0.1:<8080_PORT>/webstart.jnlp
e.g.,
        127.0.0.1:32771/webstart.jnlp

1. Provide the following configuration:
        host: https://localhost:<8443_PORT>
        username: admin
        password: admin
        
----------------------------------------------------------

Notes: 

- Docker must be running:

- If you would like to run Mirth Shell, first copy the image name from `docker ps` and then run:
        docker run -it --link <image_name>:mirth-connect marlycormar/mirth-connect-3.5.1 java -jar mirth-cli-launcher.jar -a https://mirth-connect:8443 -u admin -p admin