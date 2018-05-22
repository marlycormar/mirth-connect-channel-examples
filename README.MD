# MIRTH CONNECT EXAMPLES ON DOCKER
`Authors: Marly Cormar, Surya Prasanna.`

## Prerequisites
- The latest [Java Runtime Environment](https://www.java.com/en/).

## Current Examples
The goal of this multi-container docker is to test the functionalities of Mirth Connect.

Channels included:

1. **json_to_hl7_dest_channel_writer**: This channel receives a `json` file over an `HTTP` request, transforms it into an `hl7` message, and sends it to another channel.

        Datatype: JSON -> HL7v2.x, HL7v2.x -> HL7v2.x
        Source: HTTP Listener
        Source Transformer: json to hl7
        Destination: Channel Writer

1. **hl7FileReader_to_dbWriter**: Reads a file containing an `hl7` message and updates a mysql db accordingly.

        Datatype: HL7v2.x
        Source: File Reader
        Destination Transformer: creates steps from the hl7 template
        Destination: Database Writer

1. **secure_json_to_hl7_dest_channel_writer**: This channel receives a `json` file over an `HTTP` request, transforms it into an `hl7` message, and sends it to another channel. Optionally, you may change/add credentials to secure the connection. Please see the documentation on `channels/secure_json_to_hl7_dest_channel_writer`.

        Datatype: JSON -> HL7v2.x, HL7v2.x -> HL7v2.x
        Source: HTTP Listener
        Source Transformer: json to hl7
        Destination: Channel Writer


## Configuration
1. Create all the containers in detached mode:

        docker-compose up -d

1. Open Mirth Connect by double clicking file **webstart.jnlp**. Use credentials:

        https://0.0.0.0:8443
        admin
        admin

1. Once Mirth Connect is open, we need to import the example channel. Click on **Channels** located on left menu.

1. Also on the left menu, click **Import Channel** and add the channel `./mirth-connect/channel.xml`

1. Deploy channel.

## Web Interface

- Admin interface at:

        https://127.0.0.1:8443/webadmin/DashboardStatistics.action
    
- Channel interface at:

        https://127.0.0.1:8443/api/

## Troubleshoot
If the java applet **webstart.jnlp** fails to connect to the containers:

1. Delete the contents of the folder `data`:

        rm -r data/*
        
1. Check the ports on which the server is running:
        
        docker ps

1. Download mirth connect admin by going to:
        
        127.0.0.1:<8080_PORT>/webstart.jnlp

1. Provide the following configuration:
        
        host: https://localhost:<8443_PORT>
        username: admin
        password: admin


## Useful:

- stop all containers:

        docker stop $(docker ps -a -q) && docker rm $(docker ps -a -q) && docker volume rm $(docker volume ls)

- remove all docker containers:

        docker rm $(docker ps -a -q)

- remove all docker images:

        docker rmi $(docker images -q)

- ssh into container:

        docker exec -it <mycontainer_id> bash

- prune the system:

        docker system prune
        
- list volumes:

        docker volume ls
        
- remove volumes:

        docker volume rm $(docker volume ls)

- database credentials:

		database: mirth-test
		user: mirth
		password: password

- the local folder `./shared_folder/` is shared with the docker container that has mirth. The contents of such folder are being mapped to `/var/shared_volume` in the mirth container.

- open ports:
    - mirth-connect:

            8002->8002
            8080->8080
            8443->8443

    - mysql:

            3306->3306
