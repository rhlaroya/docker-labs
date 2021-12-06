<link rel='stylesheet' href='../assets/css/main.css'/>

# Lab : Shared Directories

## Overview

Sometimes the host and containers need to share some directories

In this example, we will share directory from host.

## Step-1 : Create a share dir

**In terminal-1 (host)**

```bash
$   cd ~/docker-labs/volumes

$   mkdir data

$   echo 'hi from host' > data/host.txt

```

## Step-2: Attach the directory to the container

**In terminal-2**

When mounting shared directories, it is recommended to use full path names.

```bash
$   echo $(pwd)/data
```

```bash
$   docker run -it --rm -v $(pwd)/data:/data alpine
```

## Step-3: Inspect the mount

Inside the container, verify the volume is mounted as `/data/` directory

```bash
$   mount
$   mount | grep '/data'

$   df -kh | grep '/data'
```

## Step-4: See the shared data 

```bash
$   cat /data/host.txt
# you will see the host file

# now create another file
$   echo "hi from c1" > /data/c1.txt
```

Exit the container by typing `exit` or `Ctrl+d`

## Step-5: Examine the shared directory

**In terminal-1 (host)**

```bash
$   ls data
$   cat data/c1.txt
```
We see the data being shared between host and container

## Step-6: Start another container

In terminal-3

```bash
$   docker run -it --rm -v $(pwd)/data:/data alpine
```

Within the container:

```bash
$   ls /data
# you will see file a.txt

# let's create another file
$   echo 'hi from c2' > /data/c2.txt
```

In terminal-1, (host) check the files

```bash
$   ls data

# you should see all files: host.txt, c1.txt, c2.txt
```

Exit the second container by typing `exit` or `Ctrl+d`

## Step-7: Mounting volumes as read-only

You can mount the directory as read-only as well

```bash
$   docker run -it --rm -v $(pwd)/data:/data:ro alpine
```
