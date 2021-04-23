## Common aspects to deploy
```
kubectl apply -f mongo-secret.yaml
kubectl apply -f mongo-configmap.yaml
kubectl apply -f mongo-deployment.yaml
kubectl apply -f mongo-express-deployment.yaml
```
---

## Deploy mongo and mongo-express with external service

- Service should be of type Loadbalancer
- Service should have nodePort configured

```
kubectl apply -f with-external-service/mongo-express-external-service.yaml
```

**NOTE: ** In minikube, the service ip is always in a pending state. 
To open the service in a browser, execute

```
minikube service mongo-express-service
```
---

## Deploy mongo and mongo-express with ingress

We need the following to be able to communicate via ingress
- Create internal service first
  - Service should be of type ClusterIP

```
kubectl apply -f with-ingress/mongo-express-internal-service.yaml
```

- Create ingress that communicates with the internal service

```
kubectl apply -f with-ingress/mongo-express-ingress.yaml
```

- The hostname used in the ingress should be configured via DNS to map to the IP of the node
(TODO: Read up on this later)

- Create ingress controller
```
minikube addons enable ingress
```
