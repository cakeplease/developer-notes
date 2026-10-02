
*Path to the repository:*

gcloud artifacts repositories describe `<repositoryName>` \
  --location=`<repositoryLocation>` \
  --format="value(name)"

gcloud artifacts repositories describe benken-frontend \  
--location=europe-north2

*Describe a role*
gcloud iam roles describe `<roleName>` for example: roles/artifactregistry.writer

Install apache server:
sudo su
apt update
apt - y install apache2


# Gcloud - Getting Started [CMDLINE]  

  

## Check installed version  

```bash  

gcloud --version  

```  

  

## Initialize gcloud  

```bash  

gcloud init  

```  

  

Set up a new configuration:  

- Choose option `2` to create a new configuration  

- Select your existing account  

- Select the project ID (`my-command-line-project`)  

  

## View current configuration  

```bash  

gcloud config list  

```  

  

---  

  

# Playing with gcloud config set [CMDLINE]  

  

## Show active configuration  

```bash  

gcloud config list  

```  

  

## Show active account  

```bash  

gcloud config list account  

```  

  

## Invalid command  

```bash  

gcloud config list environment  

```  

  

## Show environment metric  

```bash  

gcloud config list metrics/environment  

```  

  

## Show configured project  

```bash  

gcloud config list project  

gcloud config list core/project  

```  

  

## Set default region  

```bash  

gcloud config set compute/region us-central1  

```  

  

## Verify configuration  

```bash  

gcloud config list  

```  

  

## Set default zone  

```bash  

gcloud config set compute/zone us-central1-a  

```  

  

## Verify configuration  

```bash  

gcloud config list  

```  

  

## Help  

```bash  

gcloud config --help  

```  

  

## Command-specific help  

```bash  

gcloud config list --help  

```  

  

---  

  

# Gcloud - Managing Multiple Configurations [CMDLINE]  

  

## List all configurations  

```bash  

gcloud config configurations list  

```  

  

## Show active configuration  

```bash  

gcloud config list  

```  

  

## Switch configuration  

```bash  

gcloud config configurations activate cloudshell-11869  

```  

  

## Verify active configuration  

```bash  

gcloud config list  

```  

  

## Switch back  

```bash  

gcloud config configurations activate my-first-gcloud-configuration  

```  

  

## Create a new configuration  

```bash  

gcloud config configurations create my-second-gcloud-configuration  

```  

  

## Set project  

```bash  

gcloud config set project my-command-line-project-496308  

```  

  

## Verify configuration  

```bash  

gcloud config list  

gcloud config configurations list  

```  

  

## Describe an inactive configuration  

```bash  

gcloud config configurations describe my-first-gcloud-configuration  

```  

  

---  

  

# Understanding gcloud Command Structure [CMDLINE]  

  

## Check configuration  

```bash  

gcloud config list  

```  

  

## Set default project, region, and zone  

```bash  

gcloud config set project my-command-line-project-496308  

gcloud config set compute/region us-central1  

gcloud config set compute/zone us-central1-a  

```  

  

## Verify configuration  

```bash  

gcloud config list  

```  

  

## Work with Compute Engine instances  

  

### List instances  

```bash  

gcloud compute instances list  

```  

  

### Create instance  

```bash  

gcloud compute instances create my-first-vm-from-gcloud  

```  

  

Expected error:  

- Default machine type is not available  

  

### Create instance with machine type  

```bash  

gcloud compute instances create my-first-vm-from-gcloud --machine-type=n2-standard-2  

```  

  

### List instances  

```bash  

gcloud compute instances list  

```  

  

### Describe instance  

```bash  

gcloud compute instances describe my-first-vm-from-gcloud  

```  

  

### Delete instance  

```bash  

gcloud compute instances delete my-first-vm-from-  

```  

  

## Regions and Zones  

  

### List regions  

```bash  

gcloud compute regions list  

```  

  

### List zones  

```bash  

gcloud compute zones list  

```  

  

### Filter zones by region  

```bash  

gcloud compute zones list --filter="region:us-central1"  

```  

  

### Filter multiple regions  

```bash  

gcloud compute zones list --filter="region:(us-central1 us-east1)"  

```