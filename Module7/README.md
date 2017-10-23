# Demo 3: Create docker container of "Happy Birthday K8s" application.
This Demo App was written in "go" and supposed to be pushed to docker registry.
K8s will fetch our "Happy Birthday K8s" application. from docker Registry
and deploy pod, service, deployment. Farther we going to test how Replicaton
Controller puts cluster to desired state. We will than Scale Application and
perform Rolling Update of new version of the App.

1. Create Docker image:

 Build container:

```
cd ../demo3
chmod +x ./build.sh
./build.sh
```

 Push to docker registry:

```
docker build -t archyufa/webk8sbirthday:1.0.4 .
docker push archyufa/webk8sbirthday:1.0.4
```

2. Show configs with 3 replicas.

 `cat kdemo/kdemo-dep.yaml`

3. Create Deployment:

 *Option 1:*

 `kubectl run kdemo --image=archyufa/webk8sbirthday:1.0.3 --port=8080`

 *Option 2:*

 `kubectl create -f kdemo/kdemo-dep.yaml`

4. Check pods:

 `kubectl get pods`

5. Create and than expose a Service:

 *Option 1:*

 `kubectl expose deployment/kdemo --type=NodePort`

 *Option 2:*

 `kubectl create -f kdemo/kdemo-svc.yaml`

6. Find Expose Endpoint:

```
minikube ip
kubectl get svc kdemo -o wide
kubectl describe svc/kdemo
```

## Demo of Replication Controllers and reconciliation loop

1. Open second screen and run:
`while :; do clear; k get pod; sleep 2; done`

2. Let's kill 1 container. So that we will have 2 containers out of 3.

```
kubectl get pods
kubectl delete pod
```

## Demo Scaling pods

```
kubectl scale deployment/kdemo --replicas=6
kubectl scale deployment/kdemo --replicas=9
kubectl scale deployment/kdemo --replicas=5
```

## Demo Rolling Update of app

`kubectl edit deployment/kdemo`

Change to (image: archyufa/webk8sbirthday:1.0.4)

## Rollback

```
kubectl edit deployment/kdemo
kubectl rollout
kubectl rollout undo deployment/kdemo
```
