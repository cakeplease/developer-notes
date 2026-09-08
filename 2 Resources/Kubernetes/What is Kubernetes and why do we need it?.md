Why do we need Kubernetes? 
Why do we need it?
A rabbit hole, can learn something new everyday.
Place running lot of VMs, where often one VM contained one application. Then Docker came out (containarization), people started containarazing application which means you dont need entire OS, you can let one VM run multiple applications. You didnt need to manage as many VMs. Each VM=own OS, cpu, memory is shared. Containers can be very lightweight and scalable. But what if you want multiple replicas. So they had multiple VMs with multiple docker containers. So app1 would run in each VM. How to communicate across the VMs? HAPROXY loadbalancer-> gets requests from outside (users)
![[Screenshot 2026-09-01 at 13.59.19.png|700]]

It was kind of scalable, but there were lots of VMs with lots of containers, in order to upgrade you needed to manually fix one VM at time. So kubernetes is a system to fix this issue. 

#node #workernode
Kubernetes is the operating system of the cloud. It is a bunch of VMs who are able to communicate properly with each other and to divide their workload. Instead of the proxy from the example, if you look away from network, it is still VMs, running some OS, but difference is the control plane and all of the VMs from above, are called **worker nodes**. So you can ask kubernetes, to create 3 replicas of some image (defining this in yaml file), and control plane takes the request, considering the nodes, and thinks where do i have most capacity? It will think, this node is full... maybe choose another one. In an kind of intelligent way.  
![[Screenshot 2026-09-01 at 14.05.35.png|700]]

Control plane figures stuff for you. You tell it a state, and kubernetes figures it out.
The real power is when you have application that needs to run lots of docker containers, for example 100 replicas of this image, kubernetes will scale up things for you, (add nodes) so you have enough capacity for your request. Needs proper configuration. When a container fails, kubernetes will register that and spin up a new one. Kubernetes can handle crashes. It is an intelligent way of running container work loads at scale. the power is in the fact that it will take instructions and translate that to actual running work loads, scale things up if needed.

When you can specific traffic for your application, it takes care of that. It might not run at full capacity all the time, kubernetes can take those requirments and scale things up and down in an intelligent way. There is a system in way based on cpu usage.
Distributing compute across multiple vms with ease.