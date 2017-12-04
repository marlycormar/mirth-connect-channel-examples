# MIRTH CONNECT EXAMPLE ON DOCKER
`Authors: Marly Cormar, Surya Prasanna.`

*Please note that this is a work in progress! Any suggestions/bug fixes are appreciated. *

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

	   curl -X POST --header 'Content-Type: application/xml' --header 'Accept: text/html' -d 'MSH|^~\&|EPICADT|DH|LABADT|DH|201301011226||ADT^A01|HL7MSG00001|P|2.3|EVN|A01|201301011223||PID|||MRN12346^2^M11||Noether^Emmy||19710101|F||C|1 DATICA STREET^^MADISON^WI^13001-1020|GL|(414)379-1212|(414)271-3434||S||MRN12344001^2^M10|123456789|987654^NC|' 'http://127.0.0.1:8002/api/channels/<channel_id>/messages'

Please make sure to substitute `<channel_id>` with the actual channel id, e.g. `69c079fd-1cc3-469f-8f00-b4c51638fdde`.


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
	

