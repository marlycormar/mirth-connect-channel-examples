# MIRTH CONNECT EXAMPLE ON DOCKER

1. Create all the containers in detached mode:

        docker-compose up -d
        
1. Double click file `webstart.jnlp`. Use credentials:

        admin
        admin

1. Database credientials:
		
		database: mirth-test
		database: test
		user: mirth
		password: password



## Useful commands:

- ssh into container:

        docker exec -it <mycontainer> bash

	
