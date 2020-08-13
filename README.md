# Docker Helper
> A Docker studying and experiments repository written for general purpose and knowledge spreading.

From the basic Network creation until its administration through Linux firewalls bridge.

![](assets/docker.png)

## Play with Dokcer (PWD)

> https://labs.play-with-docker.com/

## Basic Docker installation environment in a Linux Kernel Distribution

#### Uninstall Docker 

```
sudo apt-get remove docker docker-engine docker-ce docker.io
```

#### Update the apt package index

```
sudo apt-get update
```

#### Allow apt to use a repository over HTTPS

```
sudo apt-get install \ 
apt-transport -https \
ca-certificates \
curl \
software-properties-common
```

#### Add Docker’s official GPG key to apt

```
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```

#### Verify that you now have the Docker GPG key

```
sudo apt-key fingerprint 0EBFCD88
```

#### Add the Docker repository to apt
```
sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"
```

#### Re-Update the apt package index now that we have the Docker repositories added

```
sudo apt-get update
```

#### Install a specific version of Docker

```
sudo apt-get install docker-ce=17.12.0~ce-0~ubuntu
```

#### Make sure that the Docker group is already added

```
sudo groupadd docker
```

#### Add your username to the Docker group

```
sudo usermod -aG docker $USER
```

## Docker 

## The Docker Flow: Images to Container

### Creating a container through the image:

Container creation:

```
docker run -ti ubuntu:latest bash
```

Exhibiting the container's info:

```
cat /etc/lsb-release

Result:

DISTRIB_ID=Ubuntu
DISTRIB_RELEASE=20.04
DISTRIB_CODENAME=focal
DISTRIB_DESCRIPTION="Ubuntu 20.04 LTS"

```

Having a lookt at the containers through the terminal:

```
docker ps --format "{{.ID}}: {{.Command}}"

Result:

ed33a850ca43: "bash"
d4ebdfb63526: "bash"
f63e60e1364d: "/bin/sh -c /app/sta…"
```

### Docker PS options

First simple and most commonly used:

```
docker ps

expected result:

CONTAINER ID        IMAGE                       COMMAND                  CREATED             STATUS              PORTS                    NAMES
d4ebdfb63526        ubuntu                      "bash"                   21 hours ago        Up 21 hours                                  magical_ellis
f63e60e1364d        prismagraphql/prisma:1.12   "/bin/sh -c /app/sta…"   5 weeks ago         Up 2 weeks          0.0.0.0:4466->4466/tcp   prisma-graphql_prisma_1
```

Showing the latest service started through Docker ps:

```
docker ps -l --format=$FORMAT

expected result:

ID	c967ca0da755
IMAGE	ubuntu:latest
COMMAND	"bash"
CREATED	5 minutes ago
STATUS	Exited (129) 5 minutes ago
PORTS	
NAMES	hardcore_banzai
```

### Docker Commit 

Creatinbg a new container:

```
docker run -ti --name=my-image  ubuntu:latest bash 
```

Checking out the created container in another terminal window:

```
docker ps -l --format=$FORMAT
```

Creating a new file:

```
mkdir development
cd development
touch server.js
```

Listing create file:

```
ls -lsa
```

Commiting the changes made:

```
docker commit ID

expected result:
sha256:49df31330335713db87a3a54f92b395df90399ef0f809bd05a62a3eab8d77c0c
```

## Under the Hood

### Docker Networking

Starging a new Docker Image:

```
docker run -ti --net=host ubuntu:16.04 bash
```

Adding Bridge-utils through apt-get:

```
apt-get update && apt-get install bridge-utils
```

Creating a brand new Network:

```
docker network create my-new-network
```

Bridge Command:

```
brctl show
```

### Docker Firewall | Linux iptables

Adding a new image:

```
docker run -ti --rm --net=host --privileged=true  ubuntu  bash
```

Updating Linux:

```
apt-get update
```

Installing iptables:

```
apt-get install i-tables
```

Running iptables: 

```
iptables -n -L -t nat
```

Running a new image | container:

```
docker run -ti --rm -p 8080:8080 ubuntu bash  
```

### Docker Processes and cgroups

Creating Container: 

```
docker run -ti --rm --name hello ubuntu bash 
```

Inspecting Docker Container ID:

```
docker inspect --format '{{.State.Pid}}' hello
```

Killing a container by its Pid:

```
docker run -ti --rm --net=host --privileged=true  --pid=host ubuntu  bash
kill pid
```

OS X & Linux:

## Usage example


This is going to be updated very soon and it will bring lots of nice examples of Docker networking.

_For more examples and usage, please refer to the [Wiki][wiki]._

## Development setup

First of all it's important to set the `$FORMAT` variable on your OS. To do so, follow the two steps:

* 1 - On your command line terminal: 

```
source /path/to/the/file/reformat.sh
```

* 2 - Test it by running on your command line terminal:

```
echo $FORMAT 

Expectesd result:

ID	{{.ID}}
IMAGE	{{.Image}}
COMMAND	{{.Command}}
CREATED	{{.RunningFor}}
STATUS	{{.Status}}
PORTS	{{.Ports}}
NAMES	{{.Names}}

```

## Linux processes check

### Processes

Listing internel OS Linux processes:

```
ps -ef

Result:

UID   PID  PPID   C STIME   TTY           TIME CMD
    0     1     0   0  3:24PM ??         0:11.62 /sbin/launchd
    0    90     1   0  3:24PM ??         0:00.60 /usr/sbin/syslogd
    0    91     1   0  3:24PM ??         0:01.15 /usr/libexec/UserEventAgent (System)
```

Listing all the IP (Internet Protocol):

```
ip addr
```
OR

```
/sbin/ifconfig 
```

## Docker Hub

Login into Docker Hub account:

```
docker login
```

Pulling an image from `Dokcer Hub`:

```
docker pull alpine
```

Check for the existing images:

```
docker images

Expected result:

REPOSITORY             TAG                 IMAGE ID            CREATED             SIZE
alpine                 latest              a24bb4013296        1 minute ago        5.57MB
```

Adding a tag to a specific image (two parms *IMAGE ID* and *TAG NAME*):

```
docker tag a24 hub1/alpine:1
docker tag a24 hub1/alpine:2
docker tag a24 hub1/alpine:3
```

> Notice you only need to have the only first three digits of the Image ID

Testing tag created:

```
docker images

Expected result:

REPOSITORY             TAG                 IMAGE ID            CREATED             SIZE
hub1/alpine            1                   a24bb4013296        2 months ago        5.57MB
hub1/alpine            2                   a24bb4013296        2 months ago        5.57MB
hub1/alpine            3                   a24bb4013296        2 months ago        5.57MB
```

Pushing to Docker Hub:

```
docker push hub1/alpine
```

If everything went well you should able to see:

> 50644c29ef5a: Pushed

Deleting the image locally:

```
docker image rm a24
```

In case you`ve got multiple tags for this image, you may need to force its deletion:

```
docker image rm a24 -f
```

Pulling the iage from Docker Hub again:

```
docker pull hub1/alpine:1
```

## Docker Linux management


> checking Dokcer Status

```
systemctl status docker
```

> stopping Docker service

```
sudo systemctl disable docker
```

## Release History

* 0.2.1
    * CHANGE: Update docs (module code remains unchanged)
* 0.2.0
    * CHANGE: Remove `setDefaultXYZ()`
    * ADD: Add `init()`
* 0.1.1
    * FIX: Crash when calling `baz()` (Thanks @GenerousContributorName!)
* 0.1.0
    * The first proper release
    * CHANGE: Rename `foo()` to `bar()`
* 0.0.1
    * Work in progress

## Meta

Thiago Lima

Distributed under the XYZ license. See ``LICENSE`` for more information.

[https://github.com/thiagoblima/docker-helper/blob/master/LICENSE](https://github.com/thiagoblima/docker-helper/blob/master/LICENSE)

## Contributing

1. Fork it (<https://github.com/thiagoblima/docker-helper/fork>)
2. Create your feature branch (`git checkout -b feature/fooBar`)
3. Commit your changes (`git commit -am 'Add some fooBar'`)
4. Push to the branch (`git push origin feature/fooBar`)
5. Create a new Pull Request


[wiki]: https://github.com/thiagoblima/docker-helper/wiki