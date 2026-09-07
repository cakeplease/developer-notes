
Everything you do in k, you will be writing as yaml files.

k get pod `<pod-name>`-o yaml

Something you define in yaml is called **manifest**

k edit pod `<pod-name> `

Generate yaml without running it on the cluster:

k run `<NAME>` --image=`<IMAGE>` --dry-run=client -o `<OUTPUT>`

for eks: 

k run test --image=httpd --dry-run=client -o yaml

> `<filename>`.yaml

where > means redirect to a file

k create (only creates )
k apply -f `<yaml-file-name>` (detects changes between two yaml files)

then k describe pod `<pod-name>

https://kubernetes.io/docs/concepts/workloads/pods/ 

kgp -o wide (more information about the pod)