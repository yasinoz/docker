---
title: Docker Labs
lang: en
slug: index
section: index
order: 0
status: needs-review
upstream: index.md
---
Welcome to the Docker labs.

These are hands-on resources to help you learn Docker.

## Pre-reqs

 - [Set up Docker and a Git client](./setup/README.md)
 - Create a [Docker Hub](https://hub.docker.com/signup) account (free)
 - Download the lab content
    - Open a terminal (PowerShell, Bash, ZSH or whatever you use) 
    - Run: `git clone https://github.com/courselabs/docker`
    - Open the folder: `cd docker`
 - Log in to Docker Hub:
   - `docker login` -  using your Docker Hub ID 
- _Optional_
    -   Install [Visual Studio Code](https://code.visualstudio.com) (free - Windows, macOS and Linux) to browse the repo and documentation


<!-- labs:start -->

## Container Basics

Running containers, building images and working with registries.

| Lab | Time | Needs |
|---|---|---|
| [Running Containers](labs/containers/README.md) | 40 min | docker |
| [Constructing the Container Environment](labs/env/README.md) | 40 min | docker |
| [Building Container Images](labs/images/README.md) | 45 min | docker |
| [Accessing Images on Registries](labs/registries/README.md) | 30 min | docker |

## Docker Compose

Modelling and running multi-container applications.

| Lab | Time | Needs |
|---|---|---|
| [Docker Compose](labs/compose/README.md) | 45 min | docker |
| [Modelling Apps with Compose](labs/compose-model/README.md) | 45 min | docker |
| [Building Apps with Compose](labs/compose-build/README.md) | 45 min | docker |
| [Limitations of Compose](labs/compose-limits/README.md) | 35 min | docker |

## Advanced Images and Networking

Multi-stage builds and how containers talk to each other.

| Lab | Time | Needs |
|---|---|---|
| [Multi-Stage Builds](labs/multi-stage/README.md) | 40 min | docker |
| [Container Networking](labs/networking/README.md) | 40 min | docker |

## Orchestration

Running containers across multiple machines.

| Lab | Time | Needs |
|---|---|---|
| [Orchestration with Docker Swarm](labs/orchestration/README.md) | 50 min | docker |
| [Kubernetes](labs/kubernetes/README.md) | 50 min | docker |

## Real World

What breaks, and how you find out why.

| Lab | Time | Needs |
|---|---|---|
| [Troubleshooting Containerized Apps](labs/troubleshooting/README.md) | 50 min | docker |

<!-- labs:end -->

### Credits

Created by [@EltonStoneman](https://twitter.com/EltonStoneman) ([sixeyed](https://github.com/sixeyed)): Freelance Consultant and Trainer. Author of [Learn Docker in a Month of Lunches](https://www.manning.com/books/learn-docker-in-a-month-of-lunches), [Learn Kubernetes in a Month of Lunches](https://www.manning.com/books/learn-kubernetes-in-a-month-of-lunches) and [many Pluralsight courses](https://pluralsight.pxf.io/c/1197078/424552/7490?u=https%3A%2F%2Fwww.pluralsight.com%2Fauthors%2Felton-stoneman).
