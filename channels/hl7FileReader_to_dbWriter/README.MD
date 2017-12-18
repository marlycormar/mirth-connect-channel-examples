# MIRTH CONNECT EXAMPLE ON DOCKER

This channel will read all the **hl7** messages (with format *(ADT-A01) Admit a patient*) located in the container **mirth-connect** in the directory `/home/Pickup`. Each message succesfully read, will be moved to `/home/Dropoff`; otherwise, the message will be relocated to `/home/Error`. In addition, every succesfull message will be transformed and added to the table **PERSON** in the mysl db **mirth-test**.


## Setup
1. Import the example channel.

1. `ssh` into the container **mirth-connect** and `cd` into `/home/Pickup`. You will need the id of the **mirth-connect** container which you may find by running `docker ps`:

		docker exec -it <mirth-connect_container_id> bash
		cd /home/Pickup

1. Create a file with extension `.hl7` and add the following HL7 message:

		MSH|^~\&|EPICADT|DH|LABADT|DH|201301011226||ADT^A01|HL7MSG00001|P|2.3| EVN|A01|201301011223|| PID|||MRN12346^2^M11||Noether^Emmy||19710101|F||C|1 DATICA STREET^^MADISON^WI^13001-1020|GL|(414)379-1212|(414)271-3434||S||MRN12344001^2^M10|123456789|987654^NC| 

1. Deploy channel.


## Useful:

- ssh into container:

        docker exec -it <mycontainer> bash

- database credentials:

		database: mirth-test
		user: mirth
		password: password
	
