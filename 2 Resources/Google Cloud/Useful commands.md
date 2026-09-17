
*Path to the repository:*

gcloud artifacts repositories describe `<repositoryName>` \
  --location=`<repositoryLocation>` \
  --format="value(name)"

gcloud artifacts repositories describe benken-frontend \  
--location=europe-north2

*Describe a role*
gcloud iam roles describe `<roleName>` for example: roles/artifactregistry.writer


