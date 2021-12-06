<link rel='stylesheet' href='../assets/css/main.css'/>

# Lab : Container 1

## Overview

When we run a docker container, we very rarely ever start from scratch. Docker provides us an OS kernel
(such as Linux), but generally does **not** provide us with any of the other aspects of the OS we
think of.  

## Step 1: Do a Docker Pull

Docker pull will pull down a public repo from dockerhub.  Think of it like a git pull.

We are going to use a lightweight Linux container called [alpine](https://hub.docker.com/r/_/alpine/).
You can read more about it [here](https://hub.docker.com/r/_/alpine/).  It is only 5 MB in size, making
it perfect for a container.

```bash
$   docker pull alpine
```

You should get the results: 

```console
Using default tag: latest
latest: Pulling from library/alpine
ff3a5c916c92: Pull complete
Digest: sha256:7df6db5aa61ae9480f52f0b3a06a140ab98d427f86d8d5de0bedab9b8df6b1c0
Status: Downloaded newer image for alpine:latest
```

## Step 2: See the docker image we downloaded

```bash
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
hello-world         latest              e38bc07ac18e        5 weeks ago         1.85kB
alpine              latest              3fd9065eaf02        4 months ago        4.15MB
```

There you see it. Alpine.  But what do we do with it?

## Step 3: Run the Container

How do we run the container?

```bash
$   docker run alpine ls
```

And we see what we ran: as we are in the root "/" directory, we see the directories there.

```console
bin
dev
etc
home
lib
media
mnt
proc
root
run
sbin
srv
sys
tmp
usr
var
```

## Step 4: Listing Containers

Let us try to list our container.  

```bash
$   docker container ls
# or
$   docker ps
```

And we get the response:

```console
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
```

**Wait??** where's our container?  Well, our container isn't running at the moment. The command we gave it (ls) ended already. We can see the stopped container if we want like this.

```bash
$   docker container ls -a
# or
$   docker ps -a
```

```console
CONTAINER ID        IMAGE               COMMAND             CREATED              STATUS                          PORTS               NAMES
d060f9a50c7c        alpine              "ls"                About a minute ago   Exited (0) About a minute ago                       admiring_keldysh
887030cdbd7e        hello-world         "/hello"            26 minutes ago       Exited (0) 26 minutes ago                           nostalgic_lewin
```

There we go. We have two containers, both stopped.  Remember hello world? That's there. Just stopped. 

Wait, should we keep creating all these containers?  You can stop it from being created if you just want to
one-and-done a command.

```bash
$   docker container --rm ls -l
```

**=> TODO: See if what containers we have. Does the new one show up?**

## Step 5: Interactive shells

Wait, wow do I ssh to my container?  Well, you don't usually do it that way. For one thing, your container
isn't actually running right now, so if you try to ssh it won't respond.  What you probably want is an
interactive shell.

How do I do that?

```bash
$   docker run -it --rm alpine /bin/ash
# or 
$   docker container run -it --rm alpine /bin/ash
```

What does this mean?
 * -i : interactive mode
 * -t : terminal mode
 * --rm : remove container after we are done
 * /bin/ash : bash is big and needs to be installed.  ash (almquist shell) is small. We also have old-school sh.

Here is the results with a few commands:

```console
/ # echo hello
hello
/ # cd
~ # pwd
/root
~ # echo bye!
bye!
~ # exit
```

**=> TODO: You try some of your own commands.**

## Summary

So what's the point?  That we can run a mini size linux?  Well, we are about to see how we can build
on top of this. But usually we need to start somewhere.  And we need some basic place to start. 
