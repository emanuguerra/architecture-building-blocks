## Kubernetes concepts and tools

### Pod

A pod is a group of containers co-located and co-scheduled.

The containers of a pod share the same storage and network.

It is modelling a "logical host" and can be seen as a group of application containers running on the same machine.

Containers in a pod share the same IP.

Pods are described through the use of Pod Templates.

Inside a pod, containers can communicate with each other using localhost.

### Deployments

A deployment object describes a desired state.

The deployment controller is responsible to change the actual state in order to bring it to the desired state.

Deployments are used for example :

- Declare the new state of the Pods
- Roollback to an earlier version
- Scale up the deployment to enable more load
- Pause the deployment
- Rollout a new "replicaset"

Example :`the deployment below creates 3 nginx pods

- The deployment is called nginx-deployment
- It creates 3 replicated pods, as indicated by the replicas field
- The pod's template indicates a pod named "nginx" which runs the nginx:1.7.9 Docker image
- The port 80 of each container is opened 

```yaml
apiVersion: apps/v1beta2 # for versions before 1.8.0 use apps/v1beta1
kind: Deployment
metadata:
  name: nginx-deployment
  labels:
    app: nginx
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.7.9
        ports:
        - containerPort: 80
```

To create this deployment run 

```
  kubectl create -f https://raw.githubusercontent.com/kubernetes/kubernetes.github.io/master/docs/concepts/workloads/controllers/nginx-deployment.yaml
```


### Minikube

Minikube is a tool to facilitate development on Kubernetes.

It runs a single node K8S cluster on a VM.

The command `minikube start` starts the cluster.

To configure kubectl to point on minikube cluster :

    kubectl config use-context minikube
    
To read pods running on the cluster :

    kubectl get pods
    NAME                          READY     STATUS    RESTARTS   AGE
    hello-node-1038538626-kbq71   1/1       Running   1          2d

To run the dashboard application :

    minikube dashboard
    
