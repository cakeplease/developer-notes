#Pods
Smallest element in the cluster. 
Networking happens on the **pod level**, k is not connecting individual containers to each other, it connects pods. 
Each pod gets own IP address (see kpg -o wide). No IP=jobs. IP address space is limited.
By default each pod can connect to each other across the nodes.
But you can configure it, so that for example only pods in given namespace can reach each other.

Containers in pods can communicate with each other through localhost.
Pod is kind of a small lightweight VM. 
 In a pod, each container needs unique port.
 
What is needed for k to connect these pods with each other?

**CNI plugin**: container networking interface
Provides network connectivity to containers. Configures network interfaces in containers. Assigns IP addresses and sets ip and sets up routes -> IP tables on nodes.

If you have a pc, you have a network interface controller, LAN adapter (**nettverkskort**):
![[Screenshot 2026-09-03 at 09.04.48.png|366]]
you stick a wire into it, and that is how you connect to local network. This also happens on software level in container/VM, NIC network interface controller, you can see that when you use ip a inside the container. Network devices (eth0) with IP address, this is done by container networking interface CNI, it configures docker container with a way to connect. Kind of like the physical LAN adapter, CNI connects the LAN adapter to your container, and attaches a wire and connects to other containers.

In linux networking you have IPTables, every node on a cluster is a VM, running often linux, and on that node the networking is configured through IPTables, done underwater through CNI plugin. When you setup cluster from scratch, you pick CNI plugin (Cilium, Calico, Flannel). 

You can connect to VM that is running k to see what CNI you are using, you need to connect to the node. 

`rdctl shell bash`
`cd /`
`cd /etc/cni`

![[Screenshot 2026-09-03 at 09.24.59.png]]

*exit* to exit bash

#Services

A service offers a consistent address to access a set of pods.
It would be hard to keep track of the IP addresses. Consept of service is quite common. But in k it has specific application. 

**Why do we need services?**

Pods are a through away kind of thing. You should not expect a pod to have a long lifespan. It scales, updates etc. They are constantly changing and being moved across nodes. How will then the system keep track of the constantly changing IP addresses?
We should not think about individual pods, we should group them by functionality. That is a service. A grouping of pods. 
![[Screenshot 2026-09-03 at 09.31.24.png|590]]
We can for example define a frontend service, and the service figures out which pod is where. You need to point app to a service, and k will handle the rest. Likewise for backend service.


See services:

`k get service`

`k expose <deployment> <name> --port <port>` - exposes a resource as a new Kubernetes service (creates service), then you can put this into a file and update it:

`k get svc <serviceName> -o yaml > service.yaml`

Different types of services:
**ClusterID** - default, creates cluster-wide IP for the service
**NodePort service** - exposes a port on each node allowing direct access to the service through any node's IP address. *Generally not used.*
**LoadBalancer** - used for cloud providers. Will create an Azure LoadBalancer to route traffic into the cluster.

Can edit service like this:

`k edit service` ´ `<serviceName>´ 

Update service:

`k apply -f <serviceName>.yaml`


#Ingress
Make your HTTP (or HTTPS) network service available using a protocol-aware configuration mechanism, that understands web concepts like URIs, hostnames, paths, and more. The Ingress concept lets you map traffic to different backends based on rules you define via the Kubernetes API.

Ingress is a resource that exposes HTTP and HTTPS routes from outside the cluster to services within the cluster. 
Features:
- SSL/TLS termination - SSL on the website is possible because of ingress controller
- external URL
- path based routing, for eks /boomark could go to different service running on the cluster
/frontend then all of the stuff under /frontend would end up in the pods that connect to the service
Quite advanced topic. First time configuring ingress is difficult. Ingress resource just like the service resource is implemented by the ingress controller. It is a yaml file:

`k create ingress`

These resources are made possible by installing the ingress controller, most common ones are:
- nginx - high-performance HTTP web server, reverse proxy, content cache, and load balancer
- traefik
- cilium
- cloud agic

Example of ingress controller:
`kube-system   traefik          LoadBalancer   10.43.248.164   192.168.64.2   80:30841/TCP,443:31012/TCP`

Ingress has a routing rule to a service.

**URLs = Ingress**


Gateway API 
![[Pasted image 20260903125743.png|508]]

https://gateway-api.sigs.k8s.io/docs/introduction/
