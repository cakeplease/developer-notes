In this file:
- Deployments: how to create them, generate from code, managing from code, editing them under cluster (not recommended)
- Replicasets
- Detail about rollout strategies, rollout update vs recreate
- Fact that kubernetes will prevent us from destroying our application if we configure it properly

*k create deploy `<name>` --image=`<image>` --replicas=`<rep_count>` -- `<command>`*
Creates 3 replicas with unique identifiers

*k get deployments.apps*  (.apps naming convension from api server)


#Generate deploy yaml and put it in the `<filename>`.`<type>` file:
*k create deploy `<name>` --image=`<image>` --replicas=`<rep_count>` --dry-run=client -o `<type> > <filename>`.`<type>`*

*k apply -f `<filename>`.yaml* (creates deployment)

Instead of saying create 10 pods, you say that you want to have 10 pods up and running.
Deploy is not creating pods, it controls the replica set. A replica set is a set of replicas of certain pod.

*k describe replicaset.apps `<name>`*

current/desired

Replicas shall not be managed by users. It is managed by deployments. But you need to be aware of replica set. 
You can have a deployment with multiple replica sets, and the old ones can still be kept around while the new ones are the active ones.

#Strategy 

`.spec.strategy` specifies the strategy used to replace old Pods by new ones. `.spec.strategy.type` can be "Recreate" or "RollingUpdate". "RollingUpdate" is the default value.

**Recreate Deployment**
All existing Pods are killed before new ones are created when `.spec.strategy.type==Recreate`.

**Rolling Update Deployment**
The Deployment updates Pods in a rolling update fashion (gradually scale down the old ReplicaSets and scale up the new one) when `.spec.strategy.type==RollingUpdate`. You can specify `maxUnavailable` and `maxSurge` to control the rolling update process.


Deployment handles operations itself. 
If you want to do updates to yaml config file, it takes care of creating new pods, and terminating old ones automatically.

**max unavailable**: is an optional field that specifies the maximum number of Pods that can be unavailable during the update process. For example: If I have app and know that I need 8 pods to be around at all time, and I have total of 10 then max unavailable is 2.

**maxSurge**:an optional field that specifies the maximum number of Pods that can be created over the desired number of Pods, example: I want 10 replicas, if maxSurge is 1, then it can only go up to 11.

So if we have 10 replicas, and max surge is 1 and max unavailable is 1, then we say that we want 10-1 pods to always be running, while the total count of pods we allow is 10+1 so there will be 9 up running while the rest (2) will either be creating or terminating.

*watch -n 1 "kubectl get pods"* (watch every second and run following command)
*k apply -f deploy.yaml*

If there is a problem with a deployment file, kubernetes will stop the deployment.
It detects that containers are not coming up, so therefore it is not going to proceed with the deployment. RunContainerError ->CrashLoopBackOff



