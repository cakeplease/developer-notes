
https://www.youtube.com/watch?v=PCYAeu9BuT8

*What is it that the dev team gets, if they build app using NAIS that they don't get otherwise?*

You build it, you run it. Other platforms would require more manual processes. In Nais, it gets automated to an extent degree. The new platform introduces cut in the process, where you don't have the separate automation team. Manageable set of services/ app that they are in charge of, don't need to coordinate too much with other teams. Whole point is that the dev team does not need all of the knowledge about devops, it should be easy. Providing higher level abstractions, extending Kubernetes API combining the Kubernetes resources. The minimum is condensed to get an app running. 

*What to do when troubles occur? How to know if the problem lies in your work or the platform?*

Focus is on the deployment interface. Operation side - don't need to how to specify resources, but you should know something about them like what is a pod etc. logs, metrics, helpful with error messages, check application logs. Most probably it is the error on the application side. In some cases you need to check the status of the pods, is it running out of memory etc. Not easy to know if all of the components are configured correctly. Proper developer portal, better overview, better insight into app. Using data, combined with algorithms, to predict scale up possibilities, translated to euros to give an impression of the actual cost. Scaling down is very difficult.

*Creating app from a template*

There is no one template to rule them all. Nais gives lot of autonomy and flexibility to the dev teams. There are some common things across the teams, but the diversity is too big to come up with one template for all of them. Hard to come up with what is a sensible starting application. Could have done it in the beginning, but now there are too many kinds of applications. And the amount of boiler plate is minimal. In most cases you need a docker file and yaml manifest, from the platform's point of view there is not anything else you actually need. 