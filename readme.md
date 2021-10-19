# Blue Green Deployment strategy using Kubernates

Deployment of new environment "Green" over the old environment "Blue" using Kubernates deployments and services.

For the demo the blue and green apps are container images of litterally green and blue apps :p

PS: We first run docker compose to build the two images locally.

PS: exist a lots of ways to acheive Bleu-Green Deployment using Kubernates. Our way uses services and deployments.

## Create the blue environment 

1. Run `docker-compose build` to build the blue and green images that will be used for this demo.

1. Create the blue deployment:

    `kubectl create -f nginx-blue.deployment.yml`

1. Create the main Service (port 80):

    `kubectl apply -f nginx.service.yml`

PS: main service expose the blue image at the begining

## Create and Test the green environment

1. Create the green deployment:

    `kubectl create -f nginx-green.deployment.yml`

1. Create the green test Service: (to test green app is working correctly before changing)

    `kubectl apply -f nginx-test.service.yml`

1. Visit `http://localhost:9000` to ensure the green app is working correctly. 

## Changing the environement from blue to green 

1. change the version attribute in nginx.service.yml to "green" and run :

    `kubectl apply -f nginx.service.yml`

## Clean

1. Delete the green test service and blue deployment once done.

    `kubectl delete -f nginx-test.service.yml`

    `kubectl delete -f nginx-blue.deployment.yml`


## Additional commands you may need :)


get informations you like:
```
kubectl get all
kubectl get pods -o wide
kubectl describe svc my-nginx
```


ssh to a pod:
```
Kubectl exec [pod-name] -it sh
```
