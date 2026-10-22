---
title: Running Containers
lang: en
slug: containers
section: basics
order: 1
duration: 40
requires: [docker]
status: needs-review
upstream: labs/containers
---
# Running Containers

Containers are a virtual computing environment which Docker creates. When you run a container it typically runs a single process, and you can have that process running in different ways.

<!-- orientation:auto -->
## How this lab works

Read this once - every lab in this track follows the same rules.

**Where you type the commands.** Open a terminal and go to the folder where you
cloned this repository. On Windows use **PowerShell** (search for it in the
Start menu), on macOS or Linux use **Terminal**. Every path in this lab is
written from the repository root, so stay there unless a step says otherwise.

**Lines starting with `>` are explanations, not commands.** Don't paste them.
Only the text inside grey code boxes gets typed.

**The 📋 sign means it's your turn.** When you see it, try the step yourself
first. Underneath it there is a collapsed **"Not sure how?"** arrow with the
answer - open it *after* you have tried, not before. The labs are written this
way on purpose: you remember what you worked out, not what you pasted.

**If a command fails, that is normal.** Some steps fail deliberately to show
you what the error looks like. Read the sentence above the command before you
assume something is broken.

**When you get stuck**, in this order:

1. Re-read the paragraph above the command - the answer is usually there.
2. Open the **"Not sure how?"** arrow.
3. Open `hints.md` for a nudge.
4. Open `solution.md` for the full answer. Using it is fine; copying it without
   reading is not.

**When you finish**, run the **Cleanup** section at the bottom. Labs share
ports and container names, so leftovers from one lab break the next one.
<!-- /orientation:auto -->

<!-- prereqs:auto -->
## Before you start

Takes about 40 minutes.

**Docker Desktop** must be running. Check it:

```
docker version
```

A `Server:` section in the output means you are ready. If you get an error
instead, start Docker Desktop and wait until the whale icon stops animating.

> Run every command from the **root of this repository** - the paths in this lab are written relative to it.

## CLI Reference

- [Docker command line reference](https://docs.docker.com/engine/reference/commandline/cli/)
- [Container commands](https://docs.docker.com/engine/reference/commandline/container/)
- [docker run](https://docs.docker.com/engine/reference/commandline/run/)

<details>
  <summary>CLI overview</summary>

The Docker command line sends instructions to the Docker API. 

Commands are grouped by types of object (e.g. containers and networks). You can always print help to list the available commands and the options for a specific command:

```
docker

docker container --help

docker container run --help
```
</details><br/>

## Running a one-off container

Docker containers run as long as the process inside the container keeps running. When the process finishes, the container exits.

You can run a simple container to run a single Linux command:

```
docker run alpine hostname
```

- lots of Docker commands have aliases - `docker run` is the same as `docker container run`.

> You'll see a lot of output when you run this - Docker pulls the Alpine Linux container image so it can run locally, starts a container, runs the hostname command and prints the output.

📋 Run another container with the same hostname command.

<details>
  <summary>Not sure how?</summary>

Just repeat the same command:

```
docker run alpine hostname
```

</details><br/>

> The container image doesn't get pulled this time, but this is a new container. The output is a different host name.

Those containers ran a single command - printing the name of the machine, which is set by Docker. When the process completed, the container exited.

📋 Print a list of all your containers.

<details>
  <summary>Not sure how?</summary>

```
# print running containers:
docker container ls

# or use ps
docker ps 

# the -a flag shows all statuses
docker ps -a
```

</details><br/>

> You have two containers, both in the exited state. The container IDs match the hostname output - when Docker creates a container it assigns a random ID and sets it as the machine name.

Those containers didn't do anything useful, but  one-off containers can be good for automation tasks, they can be packaged with all the tools and scripts they need.

Try a container which generates a security certiicate you can use for HTTPS in dev environments:

```
docker run -it ghcr.io/yasinoz/kiamol/ch15-cert-generator:latest
```

> The `-it` flag attaches your terminal, so you can send commands to the container. When you see the output `Certs generated`, exit the container by pressing Ctrl-C / Cmd-C.

📋 The cert-generator container has exited; print out the logs from the process.

<details>
  <summary>Not sure how?</summary>

```
docker container ls -a  # to find the container ID

docker container logs <container-id>
```

</details><br/>


> Container logs are the output from the container process - Docker saves them when the container exits.

The cert-generator image packages the OpenSSH library with a script to generate HTTPS certificates for a set of domains, with default settings. You'd need to install the libraries and download the script to get the same result without Docker.

## Running an interactive container

One-off containers run and then stop. You can run a long-running process in a container instead, and connect your terminal to the container's terminal.

This is like connecting to a remote machine - any commands you run actually run inside the container:

```
docker run -it alpine
```

- the `-it` flag means runs interactively, with the local terminal attached, and the default command for the Alpine container is to run the Linux shell

Now you're connected to the container, you can explore the environment:

```
ls /
whoami
hostname
cat /etc/os-release

exit
```

> You can see the container behaves like a full Linux machine, running Alpine Linux.

Linux OS containers for Docker usually have the bare-minimum toolset installed.

The Ubuntu team publish a package for Ubuntu Server but it doesn't have all the usual tools installed. There's no [curl](https://curl.se) so you can't make HTTP calls, but the container runs as the root user so you have permissions to install anything you need:

```
docker run -it ubuntu

curl https://docker.courselabs.co   # command not found

apt-get install -y curl  # this doesn't work - there's no install cache

apt-get update  # update the cache

apt-get install -y curl  # now this works

curl https://docker.courselabs.co

exit
```

> The changes you've made are only for that one container.

📋 Run another Ubuntu container and see if it can use curl.

<details>
  <summary>Not sure how?</summary>

```
# you can do this as a one-off container - it won't work:
docker run ubuntu bash -c 'curl https://docker.courselabs.co'
```

</details><br/>

Containers are isolated - the changes you made to add curl were in a different container. A new Ubuntu container starts with the clean Ubuntu setup.

Interactive containers can do fun things with the screen - this is useful to impress people with your hacking skills :)

```
docker run -it ghcr.io/yasinoz/sixeyed/hollywood:latest

# Ctrl-C / Cmd-C to stop the process

# and exit the container
exit
```

## Running a background container

Interactive containers are great for testing commands and exploring the container setup, but mostly you'll want to run _detached_ containers.

These run in the background, so the container keeps running until the application process exits, or you stop the container.

You'll use background containers for web servers, batch processes, databases message queues and any other server process.

Try running the [Nginx](https://nginx.org) web server in a container:

```
docker run -d -P --name nginx1 ghcr.io/yasinoz/library/nginx:alpine
```

- the `-d` flag runs a detached background container
- `-P` publishes network ports so you can send traffic into the container
- `--name` gives the container a name so you can work with it in other commands

> You now have a simple web server running in the container called `nginx1`.

📋 Find out which port the container is listening on, and try browsing to the web server.

<details>
  <summary>Not sure how?</summary>

```
# print the container's port mapping
docker container port nginx1

# browse to the port with curl or your browser
curl localhost:<container-port>
```

</details><br/>

> Docker listens for incoming traffic on your machine's network port and forwards it to the container.

## Lab

We've run containers using Alpine Linux and Ubuntu, and also with Nginx installed. They're all public packages available on [Docker Hub](https://hub.docker.com).

In this lab you'll work with Java containers:

- find a package on Docker Hub which you can use to run a Java app
- run a Java container and confirm which version of Java is installed using the `java -version` command
- now find a *small* image for Java, with just the JRE runtime installed

> Stuck? Try [hints](hints.md) or check the [solution](solution.md).

___
<!-- troubleshooting:auto -->
## If something goes wrong

**`Cannot connect to the Docker daemon`** - Docker Desktop is not running.
Start it and wait until the whale icon stops animating.

**`port is already allocated`** - a container from an earlier lab is still
holding that port. See what is running with `docker ps`, then remove the old
container with `docker rm -f <name>`.

**`The container name "/..." is already in use`** - same cause, same fix:
`docker rm -f <name>`, then run the command again.

**`unable to prepare context: path ... not found`** on a build - you are in the
wrong folder. Every command in this lab assumes you are at the root of this
repository.

**A `docker run` that prints usage text instead of working** - some commands in
this lab are meant to fail, to show you what a wrong argument looks like. Read
the text around the command before assuming it is broken.

Still stuck? The **Cleanup** section below resets everything, so you can start
the lab again from a clean machine.


## Cleanup

Cleanup by removing all containers:

```
docker rm -f $(docker ps -aq)
```

> On **PowerShell** the command substitution syntax is different:
>
> ```
> docker rm -f @(docker ps -aq)
> ```
>
> ⚠️ Either version removes **every** container on your machine, not just the
> ones from this lab. Run `docker ps` first if you have other work running.
