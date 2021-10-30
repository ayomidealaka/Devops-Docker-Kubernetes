# Devops-Docker-Kubernetes

[![CircleCI](https://circleci.com/gh/ayomidealaka/Devops-Docker-Kubernetes/tree/main.svg?style=svg)](https://circleci.com/gh/ayomidealaka/Devops-Docker-Kubernetes/tree/main)

# Operationalize a Machine Learning Microservice API

This is a repository for Project 4 of the **Cloud DevOps Engineer Nanodegree Program**.

The project's goal is to operationalize a pre-trained, `sklearn` model that has been trained to predict housing prices in Boston according to several features, such as average rooms in a home and data about highway access, teacher-to-pupil ratios, and so on using [kubernetes](https://kubernetes.io/), which is an open-source system for automating the management of containerized applications.

## Instructions

- Create a local environment using the following commands:

  ```
  	python3 -m venv ~/.devops
  	source ~/.devops/bin/activate
  ```

  At this point your command line should look something like:
  `(.devops) <User>:project-ml-microservice-kubernetes<user>$`. The `(.devops)` indicates that your environment has been activated, and you can proceed with further package installations.

- Install dependencies via project `Makefile`. Many of the project dependencies are listed in the file `requirements.txt`; these can be installed using `pip` commands in the provided `Makefile`. While in your virtual environment directory, type the following command to install these dependencies.

  ```
  make install
  ```

- Run python scripts using the command:
  ```
    make file
  ```
- Lint python files and docker files using the command:
  ```
    make lint
  ```
- Run webapp image using

  ```
  ./run_docker.sh
  ```

  and then run

  ```
   ./make_predictions.sh
  ```

  in a separate terminal. Check output in first terminal.

## Summary of Repository files
All files can be found in the [project-ml-microservice-kubernetes](https://github.com/ayomidealaka/Devops-Docker-Kubernetes/tree/main/project-ml-microservice-kubernetes) folder except the [circleci](https://github.com/ayomidealaka/Devops-Docker-Kubernetes/tree/main/.circleci) folder.

- **requirements.txt** - This text file has a list of package dependencies for `app.py`
- **Makefile** - This file contains the setup, install, test and lint instructions for the virtual environment
- **run_docker.sh** - This script file creates a docker image. It contains instructions on the image name, tag etc.
  - Dockerfile will copy `app.py`, install all dependencies listed in requirements.txt file and expose port 80 where the app is running.
  - The script will build docker image using `--tag=ayoalaka/project-ml-microservice-kubernetes `.
  - Built images can then be checked using `docker image ls` .
  - `docker run -p 8000:80` exposes the app at port 8000
- **upload_docker.sh** - This script uploads docker image to DockerHub by authenticating DockerHub credentials.
- **run_kubernetes.sh** - This script runs the docker image in a Kubernetes cluster.
  - `kubectl create deployment` command creates deployment.
  - `kubectl get pods` can be used to checks the state of all available pods.
  - `kubectl port-forward project-ml-microservice-kubernetes 8000:80` allows all application requests to be handled at port 8000.
- Use `./make_prediction.sh` to send input data to docker image in kubernetes pod and receive house pricing predictions.
- **.circleci/config.yml** - contains circleci config.yml script to automate `make install` and `make lint` using continuous integration with Github.
