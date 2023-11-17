# docker_manage
A script for conveniently performing backups and updates in Docker Compose Stacks.

## Description
The docker_manage script can create backups of Docker Compose stacks, including the docker-compose.yml, bind volumes, .env file, etc. It can also download new available images for all containers in the stack and thus update it. The original idea and script logic comes from a blog article by [linuxserver.io](https://www.linuxserver.io/blog/2019-10-01-updating-and-backing-up-docker-containers-with-version-control), but in the meantime I have extended it with further functions.

**Feature dump**
* Save the images [digest](https://docs.docker.com/engine/reference/commandline/images/#digests) for containers in use to keep an exact record of the current version.
* Backup the entire stack, including all files and directories that are necessary for a restore.
* Store backups of multiple stacks in a central location, sortable by stack name and date created.
* Define how many backups of a stack are to be kept.
* Minimal downtime in mind.
* Optional use of pigz (instead of gzip) for even more time savings
* Progress bar with pv for all time-consuming tasks
* Dynamic selection between docker-compose and docker compose
* Prune dangling images after the update to save storage space.

**Ideas for future versions**
* restore function - Restore a backup of choice to its original state
* freeze function - Modify a restored docker-compose.yml to use the images digest
* resume function - Return to the original image tags in docker-compose.yml

## Requirements
This script works best with Docker Compose Stacks created on the command line. The docker-compose.yml and all required files should be located in a folder with the name of the stack. Volumes for the containers should be located as bind mounts (not as named volumes) in a subfolder.

Example:
```
/opt/stack_immich/
├── appdata
│   ├── database
│   │   └── data
│   ├── immich-machine-learning
│   │   └── cache
│   └── typesense
│       └── data
├── docker-compose.yml
├── .env
└── versions.txt
```

## Setup
Save the script under `/usr/local/sbin/docker_manage` and make it executable. Then, adjust the following settings at the beginning of the script.

`APPDATA_FOLDER_NAME="appdata"`  - The name of the folder which your bind volumes are stored in  
`BACKUP_LOCATION="/opt/backups"` - The location you want to store the backups (absolute, without trailing "/")  
`BACKUP_KEEP=5`                  - The number of previous backups to keep

## Usage
Run `docker_manage {backup|update}`  
`backup` - Backup only  
`update` - Backup and update