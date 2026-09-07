
Deploy infra (for example NAIS)
https://docs.nais.io/build/reference/nais-deploy/

Build container
PR build-scan:
-docker build
-docker tag
-scan

Job: push (merge)
-docker build
-docker login
-docker push

Deploy to Kubernetes
job: deploy-dev (merge)
-az login
-connect to cluster
-kubectl apply -f yaml-file
-scan cluster config

job: deploy-prod
-approve
-same as job deploy-dev

K8s = Kubernetes itself
K3s = Small Kubernetes
K9s = UI for Kubernetes

Azure Container Apps Build and Deploy - github action
https://github.com/marketplace/actions/azure-container-apps-build-and-deploy