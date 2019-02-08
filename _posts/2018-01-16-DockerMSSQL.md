---
layout: post
title:  "Docker – How to run MSSQL Server Express"
date:   2018-01-16 21:42:46 +0000
categories: Docker
tags: [docker, MSSQL express]
---
**This tutorial presents how to run MSSQL Server Express container in the Windows 10 environment.**

# Step 1

Firstly install Docker app. You can download it and read more on [Docker web page](https://hub.docker.com/editions/community/docker-ce-desktop-windows).

# Step 2

After installation, change settings to Windows containers.

![Switch to Windows containers](/assets/SwitchToWin.png)

After changed you may have required to restarting the system.

# Step 3

Open the command prompt (personally I prefer PowerShell).
Type command:

```bash
> docker search Microsoft
```

![Containers list](/assets/ContList.png)

Type command:

```bash
> docker pull microsoft/mssql-server-windows-express
```

The downloaded SQL Server Express image includes everything we need in order to run SQL Server Express in containers.

# Step 4

Build a new container using this image.
Type command:

```bash
> docker run -d -p 1433:1433 -e sa_password=Password1* -e ACCEPT_EULA=Y microsoft/mssql-server-windows-express
```

The -d flag detaches the created container to the background. The -p flag is for port mapping. In this case creating a static mapping between port TCP:1433 of the host and TCP:1433 of the container. So the first part is for the host and the second part is for the container. The -e set environment variables are required for this particular image, and we provide parameters: sa_password=Password1* (example password for sysadmin). ACCEPT_EULA=Y agree with conditions of the licence.

# Step 5

Check running containers
Type command:

`> docker ps`

Also you can use commands:

//To show all containers use the given command:
`> docker ps -a`

//To show the latest created container (includes all states) use the given command:
`> docker ps -l`

//To show n last created containers (includes all states) use the given command:
`> docker ps -n=-1`

//To display total file sizes use the given command:
`> docker ps -s`

For more information, I encourage you to use the command:
`> docker – – help`

or visit the [Docker documentation](https://docs.docker.com/).