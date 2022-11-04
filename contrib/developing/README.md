## Developing via Container

The safest way to develop and run this repository is via the Docker container. Because we will create a predictable environment using Docker images with nodeJS in the version that this app was developed. And for that you need to have VSCode installed. And then you can use the remote access feature built into VSCode in the "ms-vscode-remote.remote-containers" extension.

Follow the step by step:

1 - Install Docker locally and VSCode.
2 - Install Docker extension, and Dev Containers extension in VsCode.
3 - Run `docker-compose up` in the path of this repository.
4 - Click on "Remote Explorer" on the side of your VSCode.
5 - In the Dropdown menu choose "Containers". It will display all running and stopped containers.
6 - Right click on "dgraph-debug" or "contrib-developing-dgraph-debug-1" and click on "Attach to Container" icon. In 1 minute or less, remote access is set up.
7 - When you see "`container golang:1.18.8-alpine3.16...`" in the left part of the footer of VsCode. Open the terminal and run the following:

```bash
go get -d -v ../dgraph

apk update

apk add --update libc-dev make gcc protobuf

optional:

apk add --update curl ca-certificates less

```

## Adding Docker

In order to run some tests you need to have Docker installed. It's a little tricky to have Docker installed inside a container. So the solution is to add sock to connect the Docker host with the Daemon inside the container. That way you can run the tests normally.

```bash
# First add the docker daemon

apk update
apk add --update docker openrc docker-compose

rc-update add docker boot

#Now run this to make sure it is running/bound

docker ps -a

```

Docker will forward few ports. You can choose to use VSCode locally or in Container. But it's important to leave the container alive. Both Local and Remote windows in the container you can write/code. As long as the connection is open, writing is bound.

PS. This was tested in Windows 11. Using Docker and WSL.