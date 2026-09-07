A Nais app lets your run one or more instances of a container image. An app is define by its application manifest (YAML file), that describes how the app should e run and what resources it needs.

https://docs.nais.io/workloads/application/

# Exposing application

Two ways to expose application:
- service discovery (for apps within the same environment)
- ingress (for users and apps outside the environment)
# Service discovery
If app and consumers run in the same env, they can communicate through service discovery. A service provides your application with n internal address that allows for direct communication within the same environment. See #Services in [[Networking fundamentals]]

Advantages:
- _Fewer network hops and lower latency_. Requests happen directly between applications. Requests to an ingress will go out of the environment to the internet, and then back to the environment.

- _Avoids unnecessary exposure_. Applications can avoid being exposed to the outside world through an ingress if all of their consumers are internal.

- _Network traffic is restricted by [access policies](https://docs.nais.io/workloads/explanations/zero-trust/)_. Access policies do not restrict inbound traffic through ingresses.

# Ingress
If your audience consists of human users or other services running in another environment, you will have to expose your application by using an ingress. See #Ingress in [[Networking fundamentals]]



