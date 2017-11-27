# MIRTH CONNECT EXAMPLE ON DOCKER

The goal of this multi-container docker is to test the functionalities of Mirth Connect. In particular, we will use Mirth Connect to read an HL7 message of type *(ADT-A01) Admit a patient* over an HTTP request, transform it, and then send it to a channel writer.

The channel `./mirth-connect/channel.xml` will read all the **hl7** messages (with format ADT-A01) sent over HTTP requests. 



## Configuration
1. Create all the containers in detached mode:

        docker-compose up -d
     
1. Open Mirth Connect by double clicking file **webstart.jnlp**. Use credentials:

        admin
        admin

1. Once Mirth Connect is open, we need to import the example channel. Click on **Channels** located on left menu.

1. Also on the left menu, click **Import Channel** and add the channel `./mirth-connect/channel.xml` 

1. Deploy channel.

1. To send an http request to the docker container, use

        curl "some message" 127.0.0.1:8002



## Useful:

- ssh into container:

        docker exec -it <mycontainer> bash

- database credentials:

		database: mirth-test
		user: mirth
		password: password
	
