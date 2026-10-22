---
title: Troubleshooting Containerized Apps
lang: en
slug: troubleshooting
section: real-world
order: 1
duration: 50
requires: [docker]
status: updated
upstream: labs/troubleshooting
---
# Troubleshooting Containerized Apps

You'll spend a lot of your time with the Docker CLI and your Compose YAML files troubleshooting problems.

The CLIs validate commands and specs for correctness when you deploy them, but they don't check that your app will actually work.

Images can be misconfigured, the container environment could be incorrect, and components might be unable to reach each other.

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

Takes about 50 minutes.

**Docker Desktop** must be running. Check it:

```
docker version
```

A `Server:` section in the output means you are ready. If you get an error
instead, start Docker Desktop and wait until the whale icon stops animating.

> Run every command from the **root of this repository** - the paths in this lab are written relative to it.

## Lab

This one is all lab :) Try running this app - and make whatever changes you need to get the app running, so the containers run and the app works.

```
docker compose -f labs/troubleshooting/compose.yml up -d
```

> Your goal is to browse to http://localhost:8090 and have a working random number generator.

Don't go straight to the solution! These are the sort of issues you will get all the time, so it's good to start working through the steps to diagnose problems.

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

When you're done you can remove all the objects:

```
docker compose -f labs/troubleshooting/compose.yml down
```
