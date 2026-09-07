Docs: https://docs.nais.io/

**NAIS** is a platform that provides developers the capability to run software in a safe and easy way. NAIS stands for Navs/Norwegian Application Infrastructure Services.

# #Team
Everything in Nais is organized around concept of a **team**. A team consists of one or more users, and at least one owner. When you create a team you will be provisioned:
- **isolated area** for team's workload and resources in each env (dev and prod)
- github team
- roles and permissions to access the teams workloads and resources

*Each env is its own Kubernetes cluster.*  Every team inside each env has its own namespace. A namespace can contain one or more workloads (applications and jobs) which are deployed in a team and are isolated from **ALL** other workloads with Kubernetes network policies. (Access denied by default approach).

![[Screenshot 2026-09-07 at 13.15.22.png]]

![[Screenshot 2026-09-07 at 14.05.53.png|433]]

# #GoodPractice
Nais applications should be inspired by the [[The Twelve-factor app manifesto]].
Here are some **good practices**: https://docs.nais.io/workloads/explanations/good-practices/

# #ImageRepository
Every team gets own image repository where they push images they run on Nais. When using [nais/docker-build-push](https://github.com/nais/docker-build-push) action in your workflow, this repo is used automatically. **Nais restricts use of images from other image registries.** To use a third-party Docker image, you must upload it to your team’s repository.


# #BuildAndDeploy

📚 [nais/docker-build-push](https://github.com/nais/docker-build-push)

📚 [nais/deploy](https://github.com/nais/deploy/tree/master/actions/deploy)

See [[Basics]] for Github actions.