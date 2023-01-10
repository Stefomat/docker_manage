# docker_manage
A script to create backups and apply updates of Docker containers in a Compose stack.

## Description
This repo contains the source code for a bash script that can be used  
to create backups of the containers and volumes in a manually set up compose stack,  
as well as pull and apply available updates to the images.
The main component is from a [linuxserver.io blog post](https://www.linuxserver.io/blog/2019-10-01-updating-and-backing-up-docker-containers-with-version-control).

## Requirements
To use this script correctly, you need a Docker Compose stack, the docker-compose.yml file, and bind volumes in a central directory.

## Setup
Adjust the following settings at the beginning of the script.

`APPDATA_LOC="/opt/appdata"` - Location of all your bind volumes.  
`COMPOSE_LOC="/opt/docker-compose.yml"` - Location of your compose file.

## Usage
Run `docker_manage {backup|update|restore|resume}`  
`backup` - Backup only  
`update` - Backup and update  
`restore` - Restore from last backup  
`resume` - Once restored from backup, go back to getting updates

## Notes
I have adapted this script for my own purposes!  
Paths, functionality, etc are adapted to work in my homelab. If you also want to use the script, I strongly recommend you to read the original blog post from [linuxserver.io](https://www.linuxserver.io/blog/2019-10-01-updating-and-backing-up-docker-containers-with-version-control). There it is also explained what the different functions of the script do exactly. This repo is just to have version control for me.
