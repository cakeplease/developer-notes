In this section:
- fundamentals about storage
- Ephemeral volumes
- Persistent volumes
- How to share volumes between containers
- How a persistent volume actually keeps on living in a cluster

# #EphemeralStorage

A container is ephemeral, you don't expect it to live long. In order to save data, you need external volume. A volume is a piece of the file system, where the container is hosted, or it can be provisioned in the cloud. There are ways of attaching the storage to container, the storage happens on the volume, separate from container where it can read and write. 

Likewise in Kubernetes, we also have volumes, portions of volume storage that are mounted to our containers. Volume is on pod level. 
Volume mount - specify which volume a container should mount.
**EmptyDir (temporary directory that shares a pod's lifetime)**

# #PersistentStorage

Persistent volumes vs persistent volumes claims

Persistent volumes is like a huge disk that is living in your cluster. Each time app needs some part of the disk, is called persistent volumes claims (territory). 
Persistent volumes can be **provisioned beforehand** or **dynamically**. Resource in the cluster just like a node. Small yaml object.

kind: PersistentVolumeClaim

Volumes are on the pod level, volume mount is on container level.

`k get pvc` (persistent volume claim)
`k get pv` (persistent volume)

#StorageClass 
StorageClass describes the parameters for a class of storage for which PersistentVolumes can be dynamically provisioned.

Lives in cluster as resource. You can:
`k get storageclasses`

local-path (takes storage from local machine) in real world it will be either on cloud or premise. It will be some third party provider. They have own storage classes. You can see in kubernetes docs. Depending on the platform, it will have a way of provisioning that storage. Like vSphere, Azure

AccessModes - if you have a deployment with several pods, and you use shared storage with "readWriteOnce", then you are forcing all pods to be scheduled on one node, because they can only access that storage from that node and you don't get the destribution over multiple nodes.


