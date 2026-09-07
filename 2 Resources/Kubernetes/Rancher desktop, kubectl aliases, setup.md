
It creates a VM on laptop, deploys kubernetes cluster and creates container env.

Traefik handles networking in cluster.

kubectl aliases

![[Screenshot 2026-09-01 at 15.33.28.png]]

Setup on mac in ./zshrc file:

**Kubectl**

alias k='kubectl'
source <(kubectl completion zsh)
compdef k=kubectl
alias kgp='kubectl get pods'
alias kc='kubectx'

then:
kubectl config current-context - see what context you are in, it should say Rancher Desktop
docker run -it ubuntu
Look for container running in rancher desktop, if not start again 

Kubernetes docs: https://kubernetes.io/docs/home/



