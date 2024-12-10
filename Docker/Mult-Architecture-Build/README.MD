### Building Multi-Architecture Docker Images 

https://docs.docker.com/reference/cli/docker/buildx/ <br>
```
sudo apt-get install docker-buildx

docker buildx --help
docker buildx ls

# Create our own buildx driver, make it default & bootstrap it
docker buildx create --name mybuilder --use --bootstrap

# Check if our builder is now the default buildx driver

docker buildx ls

# A single buildx command can be used to build & push a multi-arch docker image

docker buildx build --push \
--platform linux/amd64,linux/arm64 \
-t <tag your_docker_username</<image-name>:<tag> .

```
