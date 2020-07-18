# Docker Helper
> A Docker studying and experiments repository written for general purpose and knowledge spreading.

From the basic Network creation until its administration through Linux firewalls bridge.

![](docker.png)

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

All that you need to follow the given examples above is to have Docker properly set on your OS.

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

[https://github.com/yourname/github-link](https://github.com/dbader/)

## Contributing

1. Fork it (<https://github.com/thiagoblima/docker-helper/fork>)
2. Create your feature branch (`git checkout -b feature/fooBar`)
3. Commit your changes (`git commit -am 'Add some fooBar'`)
4. Push to the branch (`git push origin feature/fooBar`)
5. Create a new Pull Request


[wiki]: https://github.com/thiagoblima/docker-helper/wiki