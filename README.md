# aaw-docs
Documenting StatCan AAW platform

## List of tools we use

| Category                     | Tool              | Purpose                                                                                                                                                                                                                                                                                                                                       |
| ---------------------------- | ----------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Kubernetes                   | kubernetes        | In general, the entire platform is deployed on Kubernetes, so understanding the high-level concepts around working with Kubernetes is essential                                                                                                                                                                                               |
| Kubernetes                   | k3d               | Local (very) lightweight kubernetes distrobution (k3s wrapped in Docker) to quickly bootstrap local multinode clusters.                                                                                                                                                                                                                       |
| Kubernetes                   | kind              | Usually k3d is sufficient but it is very light (either alpine or distroless), so sometimes you need a more feature-full k8s distrobution (kind is debian-based)                                                                                                                                                                               |
| Containers                   | docker/containerd | K8s standardizes on containerd, but all container management stuff standardizes around the Docker API for historical reasons. Even though we don't use Docker directly, it's still important to understand the concepts around containers/images, and how image management works (building, pushing to registries, writing Dockerfiles, etc.) |
| Command line tools           | k9s               | A command-line Kubernetes dashboard.                                                                                                                                                                                                                                                                                                          |
| Command line tools           | jq                | command line JSON parser tool                                                                                                                                                                                                                                                                                                                 |
| Command line tools           | yq                | yaml parsing and formatter                                                                                                                                                                                                                                                                                                                    |
| Command line tools           | rangerfm          | command-line file system explorer.                                                                                  |
| Command line tools | kubect-np-viewer | cli tool for viewing k8s network policies |
| Command line tools | kubectl-view-webhook | cli tool to view admission webhooks |
| Command line tools | kube-lineage | cli tool to view resource ownership in kubernetes |
| Command line tools | rbac-tool | cli tool to examine kubernetes rbac |
| Command line tools | rbac-lookup | https://www.freshbrewed.science/k8s-and-krew-rbac-utilities/index.html |
| Web tools | json-to-go | https://mholt.github.io/json-to-go/ |

| Build tools                  | Makefile          | compose build logic into a single Makefile to avoid manually typing many repetitive tasks.                                                                                                                                                                                                                                                    |
| Build tools                  | Taskfile          | similar to makefile but with Yaml                                                                                                                                                                                                                                                                                                             |
| K8s Configuration management | helm              | group kubernetes configurations into a single interface (`values.yaml` file)                                                                                                                                                                                                                                                                  |
| K8s Configuration management | kustomize         | "patch" and customize kubernetes deployments                                                                                                                                                                                                                                                                                                  |
| K8s Configuration management | jsonnet           | Kubernetes configuration programming language that lets you make runtime decisions (e.g. branching logic depending on an environment variable).                                                                                                                                                                                               |
| Continuous Deployment Tools  | Argocd            | Kubernetes ready CD system that watches for changes in git repos and re-deploys to kubernetes when changes are detected                                                                                                                                                                                                                       |

**Getting Started**: Download key programs from [Install Kubernetes Tools Makefile](https://gist.github.com/blairdrummond/c147d67f78028f84f8b56a57dea337b5)

## Reading list


# High level

https://gitlab.k8s.cloud.statcan.ca/cloudnative/aaw

https://gitlab.k8s.cloud.statcan.ca/cloudnative/aaw/terraform-advanced-analytics-workspaces-infrastructure deploys dev and prod infrastructure (just infrastructure and a small number of k8s components that are managed by the cloudnative team)

https://gitlab.k8s.cloud.statcan.ca/cloudnative/aaw/terraform-advanced-analytics-workspaces-infrastructure/-/blob/main/dev_cc_00.tf E.g. node pools for AKS are specified in this terraform module

^ Other stuff like domain for dev cluster,etc.



https://gitlab.k8s.cloud.statcan.ca/cloudnative/aaw/daaas-infrastructure/aaw-dev-cc-00 This is where the core AAW platform services get deployed (bootstrap argocd apps, some stuff gets deployed through helm charts/terraform but mostly everythin gdeployed htrough ArgoCD)

https://gitlab.k8s.cloud.statcan.ca/cloudnative/aaw/daaas-infrastructure/aaw-dev-cc-00/-/blob/main/argocd_operator.tf bootstraps the root ArgoCD daaas-ysstem ArgoCD instance

^ Other ArgoCD instances are deployed from here too (e.g. org_fdi ArgoCD instance)

https://gitlab.k8s.cloud.statcan.ca/cloudnative/aaw/daaas-infrastructure/aaw-dev-cc-00/-/blob/main/argocd_operator.tf#L384-415 E.g. this is the bootstrap ArgoCD instance for the daaas-system instance



# Roadmap / Future Features

https://spiffe.io/book/

^ Spiffee - automatically injects pods with TLS certificates with information on service account, namespace, other identity info. Can federate these certificates against AAD to authenticate K8s workloads against Azure APIs. Don't need an external certificate authority; Spiffe plays the role of certificate authority.

^ E.g. Kubernetes pods can authenticate against Azure API using the identity that Spiffe provides without needing to do credential exchanges between Azure and internal secret management.


https://github.com/Azure/aad-pod-identity?msclkid=dd389aabcfc811eca5ded1ed39ef179e



