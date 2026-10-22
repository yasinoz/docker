---
title: Constructing the Container Environment
lang: en
slug: env
section: basics
order: 2
duration: 40
requires: [docker]
status: needs-review
upstream: labs/env
---
# Constructing the Container Environment

Docker creates the virtual environment for a container. You can specify how parts of the environment should be set, which lets you prepare the container for your applications.

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

Container environments are static - the details are fixed for the life of the container. You configure the environment in the `docker run` command:

- [Setting environment variables](https://docs.docker.com/engine/reference/commandline/run/#set-environment-variables--e---env---env-file)
- [Mounting volumes](https://docs.docker.com/engine/reference/commandline/run/#mount-volume--v---read-only)
- [Applying resource constraints](https://docs.docker.com/config/containers/resource_constraints/)

<details>
  <summary>CLI overview</summary>

There are dozens of options for running a container:

```
docker run --help
```

The arguments we'll use here are:

- `-e` to set the value for a single environment variable
- `--env-file` to set multiple environment variables from data in a text file
- `-v` to mount a local directory into the container's filesystem
- `--cpus` and `--memory` to specify the compute resources available to the container

</details><br/>

## Environment variables

Environment variables are key-value pairs set in the OS. Applications can read them and they're often used for configuration settings.

`printenv` is the Linux command to print them all:

```
docker run alpine printenv

docker run ghcr.io/yasinoz/library/eclipse-temurin:25-jre printenv
```

> You'll see variables set by the OS and in the container package.

📋 Run a new container - set your own environment variable and print all the variables.

<details>
  <summary>Not sure how?</summary>

```
# -e adds a new environment variable
docker run -e COURSELABS=env alpine printenv
```

</details><br/>

> Environment variables can't be edited, they're set for the lifetime of container.

You can add as many environment variables as you need, and you can also *override* default variables for the container:

```
docker run -e COURSELABS=env -e LANG=C.UTF-16 ghcr.io/yasinoz/library/eclipse-temurin:25-jre printenv
```

> This overrides the default language setting in the Java container.

If you're setting lots of variables, it's easier to store them all in a file like [exercises.env](./exercises.env) and pass that to the container as an environment file.

📋 Run container loading `labs/env/exercises.env` as an environment file.

<details>
  <summary>Not sure how?</summary>

```
# check the contents of the local file:
cat labs/env/exercises.env

# run a container loading that file as environment variables:
docker run --env-file labs/env/exercises.env alpine printenv
```

</details><br/>

> Env file contents overwrite default values, but you can overwrite them too using `-e` flags

## Container filesystem

Containers filesystems are virtual disks, put together by Docker. Every container starts with the disk contents set up in the container package.


📋 Run a background Nginx container called `nginx`.

<details>
  <summary>Not sure how?</summary>

```
# alpine is the smallest variant but any will do:
docker run -d --name nginx ghcr.io/yasinoz/library/nginx:alpine
```

</details><br/>

You can connect to a detached container and run commands in it - useful for exploring the filesystem:

```
docker exec -it nginx sh

ls /usr/share/nginx/html/

cat /usr/share/nginx/html/index.html

exit
```

> The container has the Nginx web server installed, and some default HTML pages.

You can mount a directory from your local machine into the container filesystem. You can use that to add new content, or to override existing files.

- [index.html](./html/index.html) is a web page you can display from Nginx when you mount the local folder as a volume.

Run a container to show the new web page - you need to use the full path as the source for the volume:

```
# put the full local path in a variable - on macOS/Linux:
htmlPath="${PWD}/labs/env/html"

# OR with PowerShell:
$htmlPath="${PWD}/labs/env/html"

# run a container mounting the local volume to the HTML directory:
docker run -d -p 8081:80 -v ${htmlPath}:/usr/share/nginx/html --name nginx2 ghcr.io/yasinoz/library/nginx:alpine
```

- `-v` mounts a local directory to the container - the variables store the full path and mean we can use the same Docker command on any OS

> Browse to http://localhost:8081 and you'll see the custom HTML response.

The container is reading data from your local machine. You can edit [index.html](./html/index.html) and when you refresh your browser you'll see your changes straight away.

## Compute resources

You can restrict the amount of compute power containers have. By default there's no restriction, so the container sees all the CPUs and memory your machine has.

Run a compute-intensive app without restrictions:

```
docker run -d -p 8031:80 --name pi ghcr.io/yasinoz/kiamol/ch05-pi:latest -m web 
```

- the `-m` flag gets passed to the application inside the container, it's not a container configuration.


Browse to http://localhost:8031/pi?dp=50000 - this calculates Pi to 50K decimal places. On my machine that takes ~3s.

> You can't change CPU resources for a container, they're fixed like the other environment setup.

📋 Inspect the details of the container to see the complete configuration.

<details>
  <summary>Not sure how?</summary>

```
docker inspect pi
```

</details><br/>

> All CPU and memory quotas are set to 0, meaning they're not restricted.


Try running a the same app in a container with only 200Mb of memory and 1/4 of a CPU core:

```
docker rm -f pi

docker run -d -p 8031:80 --name pi --memory 200m --cpus 0.25 ghcr.io/yasinoz/kiamol/ch05-pi:latest -m web 
```

> Refresh http://localhost:8031/pi?dp=50000 and it will take much longer - over 13s on my machine

You can print specific parts of the container configuration using [formatting](https://docs.docker.com/config/formatting/):

```
docker container inspect --format='Memory: {{.HostConfig.Memory}}b, CPU: {{.HostConfig.NanoCpus}}n' pi
```

> Memory is returned in bytes, and CPU as nano-cores (1-billionth of a core!).

## Lab

We ran a container to generate TLS certificates in the [containers lab](../containers/README.md), but the certs were created inside the container filesystem.

In this lab your job is to copy the TLS certificate and key from the container onto your local machine.

Start by generating certs in a new named container - run it in the background and the container will stay up:

```
docker run -d --name tls ghcr.io/yasinoz/kiamol/ch15-cert-generator:latest
```

Now copy the `server-cert.pem` and `server-key.pem` files from the `/certs` folder in the container onto your machine.

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
