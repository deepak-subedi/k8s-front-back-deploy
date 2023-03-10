# k8s-front-back-deploy

## STEP 1: Local Setup (create and start cluster)

refer to below link for creating local minikube cluster:
https://kubernetes.io/docs/tutorials/kubernetes-basics/create-cluster/cluster-intro/

once cluster is create, run below command to start cluster.

- minikube start

## STEP 2: Create a Secrets Object (encode secrets with base64)

refer to mongo-secrets.yaml and place encoded username and password as below with env variable "MONGO_INITDB_ROOT_USERNAME" & "MONGO_INITDB_ROOT_PASSWORD":

echo -n 'admin' | base64
YWRtaW4=

echo -n 'password' | base64
cGFzc3dvcmQ=

## STEP 3: Create a ConfigMap for Mongo Express

refer to mongodb-configmap.yaml for env vaiable "ME_CONFIG_MONGODB_SERVER"

## STEP 4: Create a Manifest for MongoDB (deployment and service)

refer to "mongo-deploy.yaml"
we are using "mongo" image

use below environment variable in deployment manifest

1. MONGO_INITDB_ROOT_USERNAME
2. MONGO_INITDB_ROOT_PASSWORD

## STEP 5: Create a Manifest for Mongo Express (deployment and external service with type LoadBalancer)

refer to mongo-express-deploy.yaml
we are using "mongo-express" image

1. ME_CONFIG_MONGODB_ADMINUSERNAME
2. ME_CONFIG_MONGODB_ADMINPASSWORD
3. ME_CONFIG_MONGODB_SERVER

## STEP 6: Port forwarding to external service with below command

This command will assign a public IP address to an external service

- minikube service mongo-express-service

## STEP 7: At last, deletes a local Kubernetes cluster after you verify all

verfify using below command (it will show all deployment, service, pods, replicasets, secrets, configmap)

- kubectl get all -n default

delete cluster using below command:

- minikube delete
