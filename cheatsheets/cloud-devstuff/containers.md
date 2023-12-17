#  Container Images 

Containers, Container Images, Container Services, and Container......

## Minimal Base Images 

-  [Google Container Tools Distroless](https://github.com/GoogleContainerTools/distrolessAlpine) 
-  Docker uses [Alpine]((https://hub.docker.com/_/alpine/)) for all official images 
-  Windows Nano Server (https://hub.docker.com/r/microsoft/nanoserver/)
-  [Docker scratc](https://hub.docker.com/_/scratch/), which can be used to build up base images or other minimalist images


## Container Tools to remove unneeded files 

-  Docker Slim (https://github.com/docker-slim/docker-slim)
-  Strip Docker Image (https://github.com/mvanholsteijn/strip-docker-image)

# Cloud Service Container Security Guides and Best Practices

- [AWS ECS Security(]https://docs.aws.amazon.com/AmazonECS/latest/bestpracticesguide/security.html)
- [AWS EKS Security(]https://docs.aws.amazon.com/eks/latest/userguide/security.html)
- [Azure Kubernetes Security Baseline(]https://docs.microsoft.com/en-us/security/benchmark/azure/baselines/aks-security-baseline)
- [GKE Configuring Cluster Security(]https://cloud.google.com/kubernetes-engine/docs/how-to/hardening-your-cluster)

## OSSTools for Kubernetes

- kubeaudit: audits Kubernetes clusters
- kube-bench: checks config against CIS Kubernetes Benchmark
- kube-hunter: hunts for security weaknesses in running cluster
- kube-score: static analysis of Kubernetes objects for security
- kubesec.io: service that scores Kubernetes resource configuration against security best practices
- conftest: unit test framework for Kubernetes config files, can be used to enforce security and operational policies
- k-rail: workload policy enforcement tool for Kubernetes
- sysdig falco: runtime anomaly detection for containers in a cluster

## Resources and References

-  [How to create the smallest possible Docker container of any image](https://xebia.com/bloghow-to-create-the-smallest-possible-docker-container-of-any-image/)
-  [Creating Smaller Docker Images](https://www.ianlewis.org/en/creating-smaller-docker-images3)
-  [simple tricks for smaller Docker images](https://learnk8s.io/blog/smaller-docker-images7 )
-  [Google best practices for building containers](https://cloud.google.com/blog/products/containers-kubernetes/7-best-practices-for-building-containers)

