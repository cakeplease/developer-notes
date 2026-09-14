List all running containers
docker ps 

List all containers
docker os -a

Stop container
docker stop `<containerName>`

Remove a stopped/exited container permanently
docker rm `<containerName/containerImage>`

Remove docker image
docker rmi `<imageName>`

List available images
docker images

Pull docker image without running it
docker pull `<imageName>`

Execute a command within a docker container
docker exec `<container>`

Clear the system
docker system prune

See history
docker history `<containerName>`

Docker caches steps under building.




