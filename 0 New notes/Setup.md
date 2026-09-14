
mac:
docker buildx build --platform amd64 -t `<imageName:tag>` .

cluster runs amd64, so correct build is needed

docker image tag SOURCE_IMAGE[:TAG] TARGET_IMAGE[:TAG] 
