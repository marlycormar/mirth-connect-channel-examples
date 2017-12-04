# MIRTH CONNECT EXAMPLES ON DOCKER
`Authors: Marly Cormar, Surya Prasanna.`

*Please note that this is a work in progress! Any suggestions/bug fixes are appreciated. *

The goal of this multi-container docker is to test the functionalities of Mirth Connect. 



## Configuration
1. Create all the containers in detached mode:

        docker-compose up -d
     
1. Open Mirth Connect by double clicking file **webstart.jnlp**. Use credentials:

        admin
        admin

1. Once Mirth Connect is open, we need to import the example channel. Click on **Channels** located on left menu.

1. Also on the left menu, click **Import Channel** and add the channel `./mirth-connect/channel.xml` 

1. Deploy channel.


## Useful:

- ssh into container:

        docker exec -it <mycontainer_id> bash

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
	
