# Top 8 Recommended Resources

## 1) About the Test
- It’s a performance-based exam: **ALL QUESTIONS** will require CLI commands, mostly with `kubectl`.
- Links:
  - [go/k8s-cka](http://goto.google.com/k8s-cka)
  - [go/k8s-ckad](http://goto.google.com/k8s-ckad)

---

## 2) IMPORTANT - Best Overall Value: Videos & Hands-On Simulations & Drills
- **Udemy Courses**:
  - [CKA with Tests](https://www.udemy.com/course/certified-kubernetes-administrator-with-practice-tests/)
  - [CKAD with Tests](https://www.udemy.com/course/certified-kubernetes-application-developer/)

---

## 3) Get Familiar with the Actual Test Environment
- **Reference Guide**:  
  [Important-Tips-CKA-CKAD-01.28.2020](https://training.linuxfoundation.org/wp-content/uploads/2019/05/Important-Tips-CKA-CKAD-4.30.19.pdf)

---

## 4) Practice Building Your Own Environment
- **Using KubeAdmin**: Easiest option and included in the test.
  - Example: Using `kubeadm` with Calico networking.
- **Kubernetes the Hard Way**:  
  A more advanced option that hardens concepts related to admin provisioning and file locations.  
  Link: [Kubernetes the Hard Way](https://github.com/kelseyhightower/kubernetes-the-hard-way)

---

## 5) Know This Documentation Like the Back of Your Hand
- [Kubectl Cheat Sheet](https://kubernetes.io/docs/reference/kubectl/cheatsheet/)

---

## 6) Know How to Locate Installation and Config Files

- Locate kubelet process:

  ```sudo ps -aux | grep kubelet```

- View systemd services for kubelet:

  ```sudo systemctl status kubelet```

- Find systemd configuration file location:

  ```/etc/systemd/system/kubelet.service.d```

- Search for active kubelet services:

  ```sudo systemctl status | grep kube```


## 7) Exercises

### Game of Pods
- [Game of Pods by KodeKloud](https://kodekloud.com/p/game-of-pods)

### Additional Practice Repositories
- [alijahnas/CKA-practice-exercises](https://github.com/alijahnas/CKA-practice-exercises)
- [stretchcloud/cka-lab-practice](https://github.com/stretchcloud/cka-lab-practice)
- [chadmcrowell/CKA-Exercises](https://github.com/chadmcrowell/CKA-Exercises)

## Linux Basics

### 8) Don’t Sleep on Your Linux Basics!  
Practice all these commands:

- **cd / ls**  
- **Find**  
- **systemctl / Systemd**  
- **vim or nano**  
- **cat**  
- **ps**

**Samples:**

```bash
# List files
ls
ls -l

# Change directories
cd /path

# Find files
find / -type f -name *crt | grep etcd or apiserver

# List processes
ps -aux | grep -i crt or certif

# Systemctl commands
systemctl list-units -all
sudo systemctl daemon-reload
sudo systemctl enable kube-apiserver kube-controller-manager kube-scheduler
sudo systemctl start kube-apiserver kube-controller-manager kube-scheduler
sudo apt-get install -y nginx
sudo systemctl restart nginx
sudo systemctl enable nginx
sudo systemctl status kube-apiserver.service kube-controller-manager.service
sudo systemctl status kubelet

# CLI shortcuts (Saving typing time)
alias k=kubectl
export do="-o yaml --dry-run=client"
```

## What is Kubernetes?

Kubernetes is an **orchestration technology** that converts isolated containers running on different hardware into a cluster.  
_“An open-source system for automating deployment, scaling, and management of containerized applications.”_

### Key Features:
- **Fault Tolerance**: Handles Pod/Node failures.
- **Auto-scaling**: Automatically scales with increased client demand.
- **Rollback**: Supports advanced deployment options.
- **Auto-healing**: Restarts crashed containers.
- **Load-balancing**: Distributes client requests efficiently.
- **Isolation**: Sandboxes ensure containers don’t interfere with each other.

---

### Other Solutions:
- **Docker Swarm**: Docker's solution based on SwarmKit.
- **Apache Mesos**: A datacenter scheduler (Marathon handles container orchestration).
- **Nomad**: Hashicorp’s lightweight orchestrator.
- **Rancher**: A container orchestrator-agnostic system.

---

## Kubernetes Architecture

A standard Kubernetes cluster includes the following components:

- **etcd**: Distributed key-value store for configuration and service discovery.  
- **weave/flannel**: Container Network Interface (CNI) for connecting services.  
- **kube-apiserver**: API server for cluster management and orchestration.  
- **kube-controller-manager**: Controls Kubernetes services.  
- **kube-discovery**: Handles service discovery.  
- **kube-dns**: DNS server for internal Kubernetes hostnames.  
- **kube-proxy**: Routes traffic through a proxy.  
- **kube-scheduler**: Assigns containers to nodes based on policies.

---

## Installation Options (4)

1. **Single-node**  
2. **Single head node with multiple workers**  
3. **Multiple head nodes with high availability (HA) and multiple workers**  
4. **HA etcd, HA head nodes, and multiple workers**

---

## Supported Environments

Kubernetes can run on:
- **BareMetal**
- **OnPrem VMs**
- **Cloud Instances**

## Kubernetes Objects for Deploying Pods

- **Pod**: Atomic unit of deployment.  
- **ReplicaSet / Replication Controller**: For scaling and healing.  
- **Deployment**: Supports versioning and rollback.  
- **Jobs**: Schedule one-time Pods to a task completion.  
- **Static Pods**: Managed directly by the kubelet daemon on a specific node.  

---

## What is a Pod?

- Smallest atomic unit of deployment in Kubernetes.  
- A Pod contains **1 or more tightly coupled containers**.  
- Pods run on a **node** controlled by the **Master (Control Plane)**.  

### Key Characteristics:
- All containers in a Pod are running, or none of them.  
- The entire Pod is hosted on the same node.  
- Pods are **ephemeral**, and their IP addresses are not persistent.  

---

## What is `kubectl`?

`kubectl` is the main CLI/API user interface into the Kubernetes **kube-apiserver**.

### Three Object Management Methods:
1. **Declarative Object Configuration**  
   - Use `.yaml` or config files only.  
   - Example:
     ```bash
     kubectl apply -f config.yaml
     ```

2. **Imperative Object Configuration**  
   - Combines `kubectl` with YAML/config files.  
   - Commands:
     ```bash
     kubectl create
     kubectl replace
     kubectl delete
     ```

3. **Imperative Commands**  
   - Direct CLI commands.  
   - Examples:
     ```bash
     kubectl run
     kubectl expose
     kubectl autoscale
     ```

---

## Declarative vs Imperative

Declarative methods define the **desired state**, while Imperative methods involve running direct commands to achieve the desired state.

---

## Kubernetes Master

The **Master Node** acts as the control plane and runs key components:  

- **Kube-scheduler**  
- **Controller-manager**  
- **Kube-apiserver**  
- **etcd**  

---

## Master Processes

The Master Node runs processes that reconcile the **desired state** with the **actual state** of the cluster.

---

## What is etcd?

- **etcd** is the cluster data store.  
- Stores configurations, metadata, and object information for Kubernetes.

---

## Kube-scheduler

- Takes actions when a new Pod is created.  
- Handles **Pod creation and management**.  
- Matches and assigns Pods to nodes based on policies.

### Advanced Scheduling Features:
- Affinities  
- Taints  
- Tolerations  

---

## Controller-manager

- Controls the **desired state** of the system.  
- Includes:
  - **Cloud-controller-manager** (for cloud environments).  
  - **Kube-controller-manager** (for on-prem environments).  

### Controllers Managed:
- Node  
- Replication  
- Route  
- Volumes  

## Kubernetes Node Runs:

- **Kubelet**:  
  Agent running on a node (minion).  
  - Listens to the master on port `10255`.  
  - Interacts with the **CRI** (Container Runtime Interface).  

- **Kube Proxy**:  
  Handles networking and routes traffic to the appropriate Pods.  

- **Container Engine**:  
  Runs on each node (minion) and works with the Kubelet.  
  - Pulls container images and starts/stops containers.  
  - Supported runtimes:
    - **Docker**  
    - **rkt**  
    - **containerd** (in progress).


## Common Commands

```bash
# Execute a command inside a Pod
kubectl exec -it <podname> -- /bin/sh

# List all Pods
kubectl get pods

# Describe a specific Pod
kubectl describe pods frontend

# Create a Pod from a YAML file
kubectl create -f resource-limited-Pod.yaml

# Delete all Pods
kubectl delete pods --all

# Scale a deployment
kubectl scale deployments first-deployment --replicas=3

# View logs of a specific Pod
kubectl logs <podname>

# List all nodes in the cluster
kubectl get nodes

# Add a label to a node
kubectl label nodes <nodename> disktype=ssd

# Print environment variables
printenv
```

## Example of Setting Up an Nginx Container

```bash
# Authenticate with the cluster
gcloud container clusters get-credentials standard-cluster-1 --zone us-central1-a

# Check for existing pods
kubectl get pods
# Output: No resources

# Create a deployment with Nginx
kubectl run first-deployment --image=nginx

# Access the Pod to make changes
kubectl exec -t first-deployment-685bdcf7bc-d7wg8 -- /bin/sh

# Add a custom message to Nginx
echo "hello nginx!" > /usr/share/nginx/html/index.html

# Update and install curl
apt-get update
apt-get install -y curl

# Test Nginx locally
curl localhost
```

## Multi-Container Pods

- **Possible**
- **Share Memory**
- **Connect with just localhost**
- **Share Volume**
- **Same ConfigMaps**

### Tightly Coupled:
- If one container crashes, all containers crash.

### Use Cases:
- SideCars  
- Proxies  
- Bridges  
- Adapters  

### Best Practices:
- Avoid packing a 3-tier architecture into 1 Pod.  
- Do not pack containers for scaling.  
- Aim for microservices with simple and independent components.  

## millicpu

- Internal Kubernetes unit, similar to vCPUs in virtual machines.  
- **millicpu**: Used for fine-grained CPU resource allocation.  

## Sample Deployment YAML File

```yaml
apiVersion: v1
kind: Pod
metadata:
   name: frontend
spec:
   containers:
   - name: db
     image: mysql
     env:
     - name: MYSQL_ROOT_PASSWORD
       value: "password"
     resources:
       requests:
         memory: "64Mi"
         cpu: "250m"
       limits:
         memory: "128Mi"
         cpu: "500m"
   - name: wp
     image: wordpress
     resources:
       requests:
         memory: "64Mi"
         cpu: "250m"
       limits:
         memory: "128Mi"
         cpu: "500m"
```

## Monitoring

```bash
# View resource usage for nodes
kubectl top node

# View resource usage for pods
kubectl top pod
```

## What are Controllers?

Controllers are **end loops** that reconcile the actual state with the desired state.  
They are managed by the **controller-manager**.

---

### Controllers for Each Object Type:
- **ReplicaSet**  
- **Deployment**  
- **DaemonSet**  
- **StatefulSet**  

---

### Key Concept:
- **Actual State <-> Desired State**: Managed through reconciliation loops.

---

## Controller Types

### ReplicaSet
- **Purpose**: Encapsulates a Pod template and ensures the desired number of replicas.  
- **Next-generation Replication Controller**:  
   - Difference: ReplicaSet supports **set-based selectors**, while Replication Controllers only support equality-based selectors.

#### Key Components:
- **Pod Selector**: Determines which Pods are managed by the ReplicaSet.  
  - All Pods with matching labels are governed.  
- **ReplicaSet Contains**:
   - Pod Template  
   - Pod Selector  
   - Labels of ReplicaSet  
   - Number of Replicas  

---

### How to Create a ReplicaSet:
```bash
kubectl apply -f replicaset.yaml
kubectl describe rs/frontend
kubectl get rs
kubectl delete rs/frontend
KUBE_EDITOR="nano" kubectl edit pod [pod-name]
```

### ReplicaSet YAML Example:
```yaml
apiVersion: apps/v1
kind: ReplicaSet
metadata:
   name: frontend
   labels:
       apps: guestbook
       tier: frontend
spec:
   replicas: 3
   selector:
       matchLabels:
           tier: frontend
       matchExpressions:
           - {key: tier, operator: In, values: [frontend]}
   template:
       metadata:
           labels:
               app: guestbook
               tier: frontend
       spec:
           containers:
           - name: php-redis
             image: gcr.io/google_samples/gb-frontend:v3
             ports:
             - containerPort: 80
```

## Deployment

- **Encapsulates ReplicaSet** template within it.  
- Supports **versioning** and **rollback**.  
- A **Deployment controller** provides declarative updates for **Pods** and **ReplicaSets**.  
- You describe a **desired state** in a Deployment object, and the Deployment controller adjusts the **actual state** at a controlled rate.  

### Deployment Magic:
- Versioning  
- Instant rollback  
- Rolling Deployment  
- Blue-green  
- Canary  

---

### Deployment Use Cases:
- **Primary**: Rollout a ReplicaSet.  
- Update an existing deployment: Pods are moved in a controlled manner.  
- Rollback to an earlier version.  
- Pause a deployment.  
- Check deployment status.  
- Clean up old ReplicaSets.  

---

### Command Example:
```bash
kubectl apply -f foo.yaml --record
```

### Field in Deployment Spec

- **Selector**  
- **Strategy**: `recreate` / `rolling update`  


### Deployment YAML Example:
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  labels:
    app: nginx
spec:
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

## Replication Controller

- Used **before Deployments and ReplicaSets**.  
- Label selector supports **equality-based selectors** (unlike ReplicaSet, which supports set-based selectors).  

---

### Replication Controller YAML Example:
```yaml
apiVersion: v1
kind: ReplicationController
metadata:
  name: example-rc
spec:
  replicas: 3
  selector:
    app: my-app
  template:
    metadata:
      labels:
        app: my-app
    spec:
      containers:
      - name: my-container
        image: nginx:latest
```
## Other Controllers

### Job Objects

- **Run-to-completion Jobs**: Used for batch processing.  
- A Job creates one or more Pods and ensures that a specified number of them successfully terminate.  
- If a Pod fails or is deleted (e.g., due to node failure), the Job starts a new Pod to ensure completion.  
- Jobs can also be used to run multiple Pods in parallel.  
- Deleting a Job will clean up the Pods it created.

**Job YAML Example**:
```yaml
apiVersion: batch/v1
kind: Job
metadata:
  name: pi
spec:
  template:
    spec:
      containers:
      - name: pi
        image: perl
        command: ["perl", "-Mbignum=bpi", "-wle", "print bpi(2000)"]
      restartPolicy: Never
  backoffLimit: 4
```

## DaemonSet

- Pod lifetime tied to that of the same node in the cluster.  
- Ensures all (or selected) Nodes run a copy of a Pod.  
- As nodes are added to the cluster, Pods are automatically scheduled.  
- As nodes are removed, the associated Pods are garbage-collected.  
- Deleting a DaemonSet will clean up the Pods it created.  

**DaemonSet YAML Example**:
```yaml
apiVersion: apps/v1
kind: DaemonSet
metadata:
  name: fluentd-elasticsearch
  namespace: kube-system
  labels:
    k8s-app: fluentd-logging
```

## Rollback

- **Every change** to the deployment template is tracked.  
- A **new revision** is created for each change.  
- Rolling back to a previous revision is simple and **trivial**.  
- Only **PodTemplate** changes are tracked.  
- **Scaling a deployment** does not create a revision.  
- Only the **PodTemplate** part is rolled back.

### Summary of Commands:
```bash
kubectl rollout undo deployment/nginx-deployment

## Summarize Commands

```bash
# Create
kubectl create -f deployment-definition.yml

# Get
kubectl get deployments

# Update
kubectl apply -f deployment-definition.yml
kubectl set image deployment/myapp-deployment nginx=nginx:1.9.1

# Status
kubectl rollout status deployment/myapp-deployment
kubectl rollout history deployment/myapp-deployment

# Rollback
kubectl rollout undo deployment/myapp-deployment
```
## Pausing Deployments

### Imperative
```bash
kubectl rollout resume deploy/nginx-deployment
kubectl rollout pause deployment/nginx-deployment
```

## Deployment Clean-Up Policy

- Cleans up old ReplicaSet versions.  
- **Default**: Retains all revisions.  
- **Set to 0**: Cleans up all revision history.  


## StatefulSet

- Manages the **deployment** and **scaling** of a set of Pods.  
- Provides guarantees about the **ordering** and **uniqueness** of these Pods.  
- Like a Deployment, a StatefulSet manages Pods based on an **identical container spec**.  
- **Unlike a Deployment**:
  - A StatefulSet maintains a **sticky identity** for each Pod.  
  - Pods are created from the same spec but are **not interchangeable**.  
  - Each Pod has a **persistent identifier** that it maintains across any rescheduling.  

## Changing Image Version, Rolling Back, and Scaling Deployments

```bash
# Changing image version
kubectl set image deployments/nginx-deployment nginx=nginx:1.9.1

# Rolling back a deployment
kubectl rollout undo deployment/nginx-deployment

# Scaling deployments imperatively
kubectl scale deployments nginx-deployment --replicas=3

# Checking deployment status
kubectl rollout status deployment/nginx-deployment
```

## What are Namespaces?

- **Namespaces** divide a physical cluster into multiple **virtual clusters**.

### Three Pre-defined Namespaces:
1. **default**: The default namespace for objects with no namespace specified.  
2. **kube-system**: Holds internal Kubernetes objects.  
3. **kube-public**: Automatically readable by all users.  

---

## What are Labels and Label Selectors?

- **Labels**:  
  - Key/value pairs attached to objects for **tagging** and **identification**.  
  - Do **not** need to be unique across objects.  
  - Labels have **no inherent semantics**.  
  - Can be applied **before** or **after** object creation.  

- **Selectors**:  
  - **Label selectors** dynamically check and match against Pod labels.  

---

## What are Annotations?

- Key/value pairs similar to labels but used for **metadata**.  
- Annotations provide information **required by the object itself**.  

## Pod Session Practice

### Quick Review of Core Concepts
Focus on ways to create Pods and Deployments during exams. Topics include:
- Creating single and multi-container Pods and Deployments.  
- Scaling Deployments.  
- Updating existing resources.  
- Basic testing and troubleshooting.

---

### Tasks:

```bash
# Create a pod named pineapple that runs nginx - imperatively
kubectl run pineapple --image=nginx

# Create a pod named watermelon that runs busybox - declaratively
kubectl apply -f - <<EOF
apiVersion: v1
kind: Pod
metadata:
  name: watermelon
spec:
  containers:
  - name: busybox
    image: busybox
EOF

# Create a pod named mango that runs image powerx to see what happens when an image does not exist
kubectl run mango --image=powerx

# Get pod IP addresses
kubectl get pods -o wide

# Create a multi-container pod named apples with 2 images: nginx and debian
kubectl apply -f - <<EOF
apiVersion: v1
kind: Pod
metadata:
  name: apples
spec:
  containers:
  - name: nginx
    image: nginx
  - name: debian
    image: debian
EOF

# Create a deployment named bananas of nginx:1.7.9 with 4 replicas
kubectl create deployment bananas --image=nginx:1.7.9 --replicas=4

# Update the bananas deployment to use nginx:1.9.1
kubectl set image deployment/bananas nginx=nginx:1.9.1
```