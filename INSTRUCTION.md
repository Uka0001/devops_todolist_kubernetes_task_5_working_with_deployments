## instructions on how to deploy the app to k8s
``` bash
cd .infrastructure
kubectl create namespace mateapp
kubectl set-context --current --namespace=mateapp
kubectl apply -f busybox.yml
kubectl apply -f clusterIp.yml
kubectl apply -f nodeport.yml
kubectl apply -f deployment.yml
kubectl apply -f hpa.yml
```

## choice of resource requests and limits
The resource requests and limits are set to 0.5 CPU and 500Mi memory. This is because the 
app is a simple to-do list app that does not require much resources to run. The app is 
also not expected to have a lot of traffic, so the resource requests and limits are set to 
a minimum to save resources and be able to test deployment and hpa configs.

## choice of HPA configuration
The HPA configuration is set to a minimum of 2 pods and a maximum of 5 pods. This is because 
the app is a simple to-do list app that does not require many resources to run. The app is also 
not expected to have a lot of traffic, so the HPA configuration is set to a minimum to save resources.

## strategy configuration (Why such numbers)
The strategy configuration is set to RollingUpdate because it is the most common strategy 
used in production environments. The strategy is set to 2 pods because the app is a simple 
to-do list app that does not require many resources to run. The app is also not expected to 
have a lot of traffic, so the strategy configuration is set to a minimum to save resources.

## how to access the app after deployment
The app can be accessed by running the following command:
``` bash
kubectl port-forward service/todoapp 8081:80 -n mateapp
```
and then opening http://localhost:8081/api in a web browser.
