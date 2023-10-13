# docker_manage
A script to create backups and apply updates of Docker containers in a Compose stack.

## Description
This repo contains the source code for a bash script that can be used  
to create backups of the containers and volumes in a manually set up compose stack,  
as well as pull and apply available updates to the images.
The initial idea is from a [linuxserver.io blog post](https://www.linuxserver.io/blog/2019-10-01-updating-and-backing-up-docker-containers-with-version-control).

## Requirements
To use this script correctly, you need a Docker Compose stack, the docker-compose.yml file, and bind volumes in a central directory.

## Setup
Adjust the following settings at the beginning of the script.

`APPDATA_FOLDER_NAME="appdata"`  - The name of the folder which your bind volumes are stored in  
`BACKUP_LOCATION="/opt/backups"` - The location you want to store the backups (absolute, without trailing "/")  
`BACKUP_KEEP=5`                  - The number of previous backups to keep

## Usage
Run `docker_manage {backup|update}`  
`backup` - Backup only  
`update` - Backup and update  

## Disclaimer
I have adapted this script for my own purposes!  
Paths, functionality, etc are adapted to work in my homelab. If you also want to use the script, I strongly recommend you to read the original blog post from [linuxserver.io](https://www.linuxserver.io/blog/2019-10-01-updating-and-backing-up-docker-containers-with-version-control). There it is also explained what the different functions of the script do exactly. This repo is just to have version control for me.
