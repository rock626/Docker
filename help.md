### Useful docker commands

- List images
	
		sudo docker images

* List containers
	
		sudo docker container ls
	
* Stop running container
	
		sudo docker container {container_name} stop
	
* Cleanup stopped containers and cache
	
		sudo docker system prune
	
* To executing any command in running container
	
		sudo docker exec -ti {container_name} bash
	
* View help for any command
	
		sudo docker {command_name} --help 
