A Kubernetes cluster is one or more nodes providing CPU, memory, and other resources for use by applications.
Kubernetes supports two node types:
- Control plane nodes
- Worker nodes
  
Control plane nodes must be Linux, but worker nodes can be Linux or Windows.Every control node runs below services

- API server
- Scheduler
- Controllers

Control plane nodes can also run user applications, but you should probably force user applications to run on worker nodes in production environments. Doing this allows control plane nodes to focus on managing the cluster.
## The control plane
### The API server:
The API server is the front end of Kubernetes, and all requests to change and query the state of the cluster go through it. Even internal control plane services communicate with each other via the API server. It exposes a RESTful API over HTTPS, and all requests are subject to authentication and authorization.

### The cluster store
The cluster store holds the desired state of all applications and cluster components and is the only stateful part of the control plane.It’s based on the etcd distributed database.

### Controllers and the controller manager
Kubernetes uses controllers to implement a lot of the cluster intelligence. They all run on the control plane.Controllers ensure the cluster runs what you asked it to run.

For example, if you ask for three replicas of an app, a controller will ensure three healthy replicas are running and take appropriate actions if they aren’t.

Kubernetes also runs a controller manager that is responsible for spawning and managing the individual controllers.

### The scheduler
The scheduler watches the API server for new work tasks and assigns them to healthy worker nodes.
It implements the following process:
1. Watch the API server for new tasks
2. Identify capable nodes
3. Assign tasks to nodes

## The Worker Nodes

### Kubelet
The kubelet is the main Kubernetes agent and handles all communication with the cluster.
It performs the following key tasks:
- Watches the API server for new tasks
- Instructs the appropriate runtime to execute tasks
- Reports the status of tasks to the API server
If a task won’t run, the kubelet reports the problem to the API server and lets the control plane decide what actions to take.

### Runtime
Every worker node has one or more runtimes for executing tasks. Most new Kubernetes clusters pre-install the containerd runtime and use it to execute
tasks. These tasks include:
- Pulling container images
- Managing lifecycle operations such as starting and stopping containers

# Kube-proxy
Every worker node runs a kube-proxy service that implements cluster networking and load balances traffic to tasks running on the node.

# 4: Working with Pods

### Pod manifest files
```
kind: Pod
apiVersion: v1
metadata:
  name: hello-pod
    labels:
    zone: prod
    version: v1
spec:
  containers:
    - name: hello-ctr
      image: nigelpoulton/k8sbook:1.0
      ports:
        - containerPort: 8080
      resources:
        limits:
          memory: 128Mi
          cpu: 0.5
```
- kind field tells Kubernetes what type of object you’re defining.
- apiVersion tells Kubernetes what version of the API to use when creating the object.
- metadata section names the Pod hello-pod and gives it two labels.
-  spec section defines details related to containers

### Deploying Pods from a manifest file
`kubectl apply -f pod.yml`

### kubectl get
- -o wide gives a few more columns but is still a single line of output
- -o yaml gets you everything Kubernetes knows about the object  
```
kubectl get pods  # Get status of all running pods
kubectl get pods hello-pod -o yaml  # Get details of specific pod
```
### kubectl describe
This gives you a nicely formatted overview of an object, including lifecycle events    
`kubectl describe pod hello-pod`

### kubectl logs
kubectl logs command to pull the logs from any container in a Pod. The basic format of the command is kubectl logs <pod>.  
If you run the command against a multi-container Pod, you automatically get the logs from the first container in the Pod. 
However, you can override this by using the -- container flag and specifying the name of the container you want the logs from  
```
kubectl logs <pod>
kubectl logs logtest --container syncer
```
