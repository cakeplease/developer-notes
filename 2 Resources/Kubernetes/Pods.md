Namespace is a way to separate things.
k run nginx-test --image=nginx
k run httpd-test --image=httpd

## What is a pod?
The smallest element on Kubernetes cluster. Smallest unit on a node.

#cluster group of machines that work together to run and manage containerized applications.

- #cluster = all machines together
- #nodes = individual machines (VMs or physical servers)
- #pods = running containers

We have a cluster with control plane, it runs on laptop in rancher desktop. 

![[Screenshot 2026-09-02 at 09.16.02.png]]

K port 6443, this is port of the API server, k cluster on control plane contains: ETCD (brain), scheduler, API server amongs other things...
API server (6443)

Rancher desktop is exposing this port and is going to route that traffic to API server that runs on this cluster. If I run command it will be sent to API server. So how does terminal know that it needs to go to API server? In the config file, it says API address: https://127.0.0.1:6443
This is the current active context (k config current-context -> rancher desktop), kubectl is reading current config, and knows it should send request to local API server. 

User -> (command, for eks: k run nginx-test --image=nginx) -> kubectl -> API server
And it then schedules a pod (using **scheduler**). You can do lots of stuff with scheduler.
API server talks to scheduler, takes in request, and makes intelligent decision. Its job is to assign pods in the node.
A pod is not a container, it's a collection of containers + other resources.

Kubernetes means helmsmen (man hwo is standing on the ship and is turning the wheel).
Sea-nautical theme
Pod of whales (group of whales), several whales form a pod.
Pod is a collection, group of containers and other resources.
Most common pod is a single container pod. 

Describe:
k describe pod `<name>`

#pod: 
- single container
- multi container
- Init container (needs to run successfully before next pod is going to run), that is how you can do some conditional deployments. 
- networking
- storage

kgp -o wide (get network info)
kgp -n (--namespace) namespace

k exec -it `<pod-name> ` -c `<containerName>` -- `<command> `(-it, interactive shell)

tree package
curl package
htop package

It is possible to explore the pods, ping each other, curl it etc.

Learn how to get more info from the pod, how to get into and explore, ping, curl.