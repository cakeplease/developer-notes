## Overview  

The Twelve-Factor App is a methodology for building modern cloud-native and SaaS applications. The goal is to create applications that are:  

- Easy to deploy  
- Easy to scale  
- Portable across environments  
- Maintainable over time  
- Suitable for continuous delivery and cloud platforms  
- Consistent between development and production environments  

Source: https://12factor.net/ 【1-f456d0】  

---  
# The 12 Factors  

## I. Codebase  

**One codebase tracked in version control, many deployments.**  

### Key Ideas  

- One application = one repository.  
- Use Git or another version control system.  
- Deploy the same codebase to different environments (dev, test, prod).  
### Example  

```text  

my-app  

├── src/  

├── tests/  

└── .git  

```  

---  

## II. Dependencies  

**Explicitly declare and isolate dependencies.**  
### Key Ideas  

- Never rely on software already installed on a server.  

- All dependencies should be defined in configuration files.  

### Examples  

Node.js:  

```json  

{  

"dependencies": {  

"express": "^5.0.0"  

}  

}  

```  


.NET:  

```xml  

<PackageReference Include="Serilog" Version="4.0.0" />  

```  

### Benefits  

- Reproducible builds  

- Easier onboarding  

- Fewer environment-specific issues  

---  
## III. Config  

**Store configuration in environment variables.**  

### Key Ideas  

- Keep secrets and environment-specific settings outside the code.  

- Never hardcode credentials.  

### Good  

```bash  

DATABASE_URL=postgres://...  

API_KEY=secret  

```  

### Bad  

```csharp  

string apiKey = "secret";  

```  

### Typical Config Values  

- Database connections  

- API keys  

- OAuth credentials  

- Feature flags  
---  

## IV. Backing Services  

**Treat backing services as attached resources.**  

### Key Ideas  

Applications should view external resources as replaceable services.  


Examples:  

- PostgreSQL  
- Redis  
- Kafka  
- RabbitMQ  
- Object Storage  

### Example  

Instead of:  

```text  

Application is tightly coupled to PostgreSQL Server A  

```  

Use:  

```text  

Application -> DATABASE_URL  

```  


The database can then be swapped without code changes.  
---

## V. Build, Release, Run  

**Strictly separate build, release and run stages.**  

### Build  

Compile and package code.  

### Release  

Combine build artifact with configuration.  

### Run  

Execute the release.  

### Pipeline Example  

```text  

Code  

↓  

Build  

↓  

Release  

↓  

Run  

```  

  
### Benefits  

- Easier rollbacks  
- Better traceability  
- More reliable deployments  

---  

## VI. Processes  
**Execute the app as one or more stateless processes.**  

### Key Ideas  

Application instances should not store persistent data locally.  

### Bad  

```text  

User uploads file  

↓  

Stored on pod filesystem  

```  

### Good  

```text  

User uploads file  

↓  

Stored in S3 / Blob Storage  

```  


### Why?  

Pods and containers may disappear at any time.  


---  

## VII. Port Binding  

**Export services via port binding.**  

### Key Ideas  

The application should expose its own HTTP service.  

### Example  

```bash  

dotnet run --urls=http://0.0.0.0:8080  

```  

Container:  

```text  

Application  

↓  

Port 8080  

↓  

Ingress  

```  

This fits naturally with Docker and Kubernetes.  

---  

## VIII. Concurrency  

**Scale out via the process model.**  
### Key Ideas  

Scale horizontally rather than vertically.  

### Vertical Scaling  

```text  

1 bigger server  

```  

### Horizontal Scaling  

```text  

Pod 1  

Pod 2  

Pod 3  

Pod 4  

```  

  

### Kubernetes Example  

  

```yaml  

replicas: 4  

```  

  

---  

  

## IX. Disposability  

**Fast startup and graceful shutdown.**  
### Key Ideas  

Applications should:  
- Start quickly  
- Shut down cleanly  
- Handle restarts safely  

  

### Why?  

Platforms like Kubernetes frequently:  

- Restart containers  
- Reschedule workloads  
- Scale replicas up/down  

### Good Shutdown Flow  
```text  

SIGTERM  

↓  

Finish requests  

↓  

Close connections  

↓  

Exit  

```  

  

---  

  

## X. Dev/Prod Parity  
**Keep development, staging and production as similar as possible.**  

### Goal  
Reduce:  

```text  

"It works on my machine"  

```  

  

### Examples  
Use:  

- Same database engine  
- Same runtime version  
- Same deployment process  


Avoid:  

- SQLite locally + PostgreSQL in production  
- Different operating systems  
- Different application versions  


---  


## XI. Logs  

**Treat logs as event streams.**  
### Key Ideas  

Applications should:  

- Write logs to stdout/stderr  

- Let the platform collect them  

### Example  
```csharp  

logger.LogInformation("User logged in");  

```  


### Platform Responsibilities  
- Aggregation  
- Storage  
- Search  
- Monitoring  

  
Examples:  
- Loki  
- Grafana  
- Elasticsearch  
- Splunk  
- Azure Monitor  
---  

  

## XII. Admin Processes  

**Run admin tasks as one-off processes.**  

### Examples  

  

Database migration:  

  

```bash  

dotnet ef database update  

```  

  

Data import:  

  

```bash  

python import.py  

```  

  

NAIS Job:  

  

```bash  

kubectl create job  

```  

### Key Idea  

  

Administrative tasks should:  

- Use the same codebase  

- Use the same configuration  

- Run separately from the main application  

  

---  

  

# Relation to Kubernetes  

The 12-Factor principles map almost perfectly to Kubernetes.  

  

| 12-Factor | Kubernetes |  

|------------|------------|  

| Config | ConfigMaps & Secrets |  

| Backing Services | PostgreSQL, Redis, Kafka |  

| Processes | Stateless Pods |  

| Port Binding | Container Ports |  

| Concurrency | Replicas |  

| Disposability | Pod Lifecycle |  

| Logs | stdout/stderr |  

| Dev/Prod Parity | Same manifests across environments |  

  

---  

  

# Relation to NAIS  

  

Many NAIS best practices are based on 12-Factor ideas.  

  

### NAIS Examples  

  

#### Config  

```yaml  

env:  

- name: API_URL  

value: https://api.example.com  

```  

  

#### Secrets  

```yaml  

envFrom:  

- secret: my-secret  

```  

  

#### Scaling  

```yaml  

replicas:  

min: 2  

max: 6  

```  

  

#### Logging  

```text  

Application -> stdout -> NAIS/Grafana  

```  

  

---  

  

# Quick Summary  

  

The five most important principles:  

  

1. Store configuration in environment variables.  

2. Keep applications stateless.  

3. Explicitly declare dependencies.  

4. Scale horizontally through multiple instances.  

5. Keep development and production environments as similar as possible.  

  

If an application follows these principles, it will generally be easier to deploy, operate, maintain, and scale in Kubernetes and NAIS environments.