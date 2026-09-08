Containers are separate environments, with own processes, network, mounts but share OS kernel. Containers have existed for a long time. 
Docker started with LXC -> libcontainer -> runc -> **containerd** (today)

## How Docker works

Tool to build, run and manage containers. Main purpose is to package applications and ship them as many times as you want.


## Containers vs VM

#VM runs a complete operating system on top of a hypervisor.

![[Screenshot 2026-09-08 at 12.45.59.png]]

#container  share the host OS kernel and only package the application and its dependencies.
![[Screenshot 2026-09-08 at 12.46.38.png]]

## Images and registries

- **Image** is a package/template, it is used to create one or more containers. 
- **Containers** are instances of images.
- **Registry** is a centralized online storage system where you can download share and manage container images.



## Good to know
**Container lives as long as the process within it does.** 