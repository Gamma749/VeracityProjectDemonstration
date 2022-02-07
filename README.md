# Veracity Project Demonstration


## About this project
This repository hosts the final demonstration of a summer research project I undertook 2021-2022. The project looked into using some modern technology in computer science to tackle veracity problems. My part of the project was to develop and investigate distributed ledger technology which would form the lower level infrastructure for another project. In this repository I finalize and present this work, and leave it open for possible extension in the future.  

## Prerequisites
Ensure that your machine runs docker and docker-compose.

## Running this project

- From the root directory, run `./manage-network up` to start the network
    - This script runs docker-compose using the yaml file in the `network` directory as config
    - Four Iroha containers (with a postgres container each) will form the blockchain infrastructure, while a redis container and a jupyter notebook server will form the front end

- The script will drop into the logs of the jupyter notebook server, which will eventually (after some startup) give a link to follow (like `http://127.0.0.1:8888/...`)

- Open this link in your preferred browser and navigate to `introduction.ipynb`

- Once finished, run `./manage-network down` to destroy the containers

## If deploying this project to a cloud instance, please follow the steps below
- run `scp -i <private-key-file> -r . ubuntu@<ip>:/home/ubuntu` (or similar for other distros)
- move to the cloud instance with `ssh -i <private-key-file> ubuntu@<ip>`
- run the following commands to set up the instance with docker and docker compose:
	- `sudo apt-get update`
	- `sudo apt-get install docker.io`
	- `sudo curl -L "https://github.com/docker/compose/releases/download/v2.2.3/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose`
	- `sudo chmod +x /usr/local/bin/docker-compose`
- Get a super user shell `sudo -s`
- Run `/home/ubuntu/manage-network up`

If you want to reset the notebooks each day, I recommend using a crontab to script this. I found the best settings were to add to the sudo crontab something like:
```
55 23 * * * /home/ubuntu/manage-network.sh down
59 23 * * * /home/ubuntu/restore-notebook-copy.sh
0 0 * * * /home/ubuntu/manage-network.sh up
```
