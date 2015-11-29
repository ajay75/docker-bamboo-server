# docker-bamboo-server
Atlassian bamboo server, version 5.1.37

## Usage

```
docker run --name bamboo -it --rm -p 8085:8085 -p 54663:54663 --net=host savaki/bamboo-server:latest
```
