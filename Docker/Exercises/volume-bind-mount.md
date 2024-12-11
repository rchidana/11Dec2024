### Exercise to store data outside the container using Volumes
### Docker Documentation : https://docs.docker.com/storage/volumes/
### Docker CLI Reference : https://docs.docker.com/engine/reference/commandline/volume_create/ 
### Bind Mount Documentation : https://docs.docker.com/storage/bind-mounts/ 

```
# Any folder from the host machine can be bind mounted to a container
# Note : In few cases, folder permissions will have to be addressed appropriately

# Let us bind mount a local folder (which is in home directory) by name 'local-folder' to a container by name 'container1'

docker run -itd --name container1 -v ~/local-folder:/local-folder alpine bin/sh
docker ps

# Get into 'container1' and write some data to '/local-folder'
docker attach container1
cd local-folder

echo "hello, from container1" >> ctr1-data.txt

# Let us spin up another new container called 'container2' which will user --containers-from option

docker run -itd --name container2 -v ~/local-folder:/local-folder alpine bin/sh

# Attach to container2 and check the contents of '/local-folder'
docker attach container2
ls /local-folder

# Try to write a new file in this folder and check if its visible in Container1
echo "hello, from container2" >> ctr2-data.txt

```

