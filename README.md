README
==============================================================================
This project presents how to create a Kubernetes deployment of the BookStoreAPI created in https://github.com/himasha/MGWDeveloperWorkflow.

![Alt text](/resources/MGWOpsFlow.png?raw=true "Optional Title")

## Prerequisites

1.Please follow the instructions in https://github.com/himasha/MGWDeveloperWorkflow in order to create and build the bookstore MGW project. 

2. Install Kubernetes,docker,kubectl.

3. Valid docker hub account. 

## Creating deployment configuration file for Development environment (Kubernetes)

1. You should be having the bookstore MGW project available after following https://github.com/himasha/MGWDeveloperWorkflow.

1. Create a Kubernetes deployment configuration file (/deployment-configs/dev_dep_config.toml) defining the deployment that is required. We will use the MGW runtime docker image as the base image and include API artifacts to it at build time. We will be creating a Kubernetes Nodeport service to expose the deployment.  

2. Any deployment configuration file created needs to be added to the MGW project's conf folder. To provide readability when multiple config files are included, let's create a folder called 'dev' inside bookstore/conf folder. 

3. Add dev_dep_config.toml file to the dev folder of bookstore/conf folder.

4. Since we are pushing the docker images to a docker hub registry, make sure that you set your docker hub username/password with following commands executed in the terminal.

export DOCKER_USERNAME= "provide username"
export DOCKER_PASSWORD= "provide password"


## Building bookstore project

1. Build the bookstore project using MGW toolkit pointing to the dev_dep_config file as the deployment configuration to be used.

`micro-gw build bookstore/ -d bookstore/conf/dev/dev_dep_config.toml`

2. This would build the artifacts and provide you with a command to execute and deploy the artifacts in Kubernetes similar to below. 

   Run the following command to deploy the Kubernetes artifacts: 

	`kubectl apply -f /Users/himasha/Documents/Demo/bookstore/target/kubernetes/bookstore`


	Run the following command to install the application using Helm: 

	`helm install --name bookstore-deployment-6730ab57-1fea-4dd4-a29c-aad0a56eddc8 /Users/himasha/Documents/Demo/bookstore/target/kubernetes/bookstore/bookstore-deployment-6730ab57-1fea-4dd4-a29c-aad0a56eddc8`


