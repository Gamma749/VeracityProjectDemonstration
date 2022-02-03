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
  - Note that the notebook server will use the password specified in `network/swipl/swipl.env`. In this repository this is currently set to no password which is very insecure! If you want to add a password to your server, please alter this file before running `manage-network up`

- Open this link in your preferred browser and navigate to `introduction.ipynb`

- Once finished, run `./manage-network down` to destroy the containers
