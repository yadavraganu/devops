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
## The Worker Nodes

### The scheduler
The scheduler watches the API server for new work tasks and assigns them to healthy worker nodes.
It implements the following process:
1. Watch the API server for new tasks
2. Identify capable nodes
3. Assign tasks to nodes
