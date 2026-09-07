Namespaces are a logical grouping of resources, a mechanism for isolating groups of resources within a single cluster. 
In Kubernetes, _namespaces_ provide a mechanism for i**solating groups of resources** within a **single cluster.** Names of resources need to be unique within a namespace, but not across namespaces. Namespace-based scoping is applicable only for namespaced [objects](https://kubernetes.io/docs/concepts/overview/working-with-objects/#kubernetes-objects) _(e.g. Deployments, Services, etc.)_ and not for cluster-wide objects _(e.g. StorageClass, Nodes, PersistentVolumes, etc.)_.

For example, team based namespaces. Every application, workload should have own namespace.
Do not use default in prod.
Similar to resource group in Azure.

*k create namespace mealie -o yaml --dry-run=client*

`apiVersion: v1`
`kind: Namespace`
`metadata:`
  `name: mealie`
`spec: {}`
`status: {}`

If you delete namespace, every resource under this namespace will be deleted!

Get all namespaces
 *k get ns*

set current namespace: 
*k config set-context --current --namespace=`<namespace>`

see current namespace:
*k config view*
see namespace under context



