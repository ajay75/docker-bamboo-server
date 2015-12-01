# docker-bamboo-server
Atlassian bamboo server, version 5.1.37

## Usage

### Startup in daemon mode

```
docker run -d \
	--name bamboo \
	-p 8085:8085 -p 54663:54663 --net=host \
	-v /bamboo-data:/var/lib/bamboo \
	savaki/bamboo-server:latest
```

### Startup in interactive mode (ctrl-c to quit)

```
docker run -it --rm \
	--name bamboo \
	-p 8085:8085 -p 54663:54663 --net=host \
	-v /bamboo-data:/var/lib/bamboo \
	savaki/bamboo-server:latest
```

