# Kubernauts Kops Faststart

---

**Kops** (Kubernetes Operations) is currently the best way for deployment, operation, upgrade and decommissioning of Kubernetes Clusters on AWS. A huge thanks to [Kris Nova](https://twitter.com/Kris__Nova) and the Kops team for this brilliant implementation.

If you’re new to Kubernetes please refer to the fantastic [Kubernetes Bootcamp](https://kubernetesbootcamp.github.io/kubernetes-bootcamp/) and learn the basics interactively with the integrated Katacoda implementation.

Note: there is a NEW exciting project “[Kubicorn](https://www.nivenly.com/kubicorn/)” from Kris Nova which you should consider to run Kubernetes on AWS and later on ANY Cloud.

This guide is based on the [Kops documentation on Github](https://github.com/kubernetes/kops/blob/master/docs/aws.md) and inspired by [Manage Kubernetes Clusters on AWS Using Kops](https://aws.amazon.com/de/blogs/compute/kubernetes-clusters-aws-kops/) by [Arun Gupta](https://twitter.com/arungupta) and some additional help from the great docs on [kubernetes.io](https://kubernetes.io) site to help you get started very fast and possibly too fast using Kops 1.6.2 to deploy multiple Kubernetes clusters on AWS. I recommend to read the great documentation on Github and enjoy Arun’s post.

This guide is the 1st part of a series and shows only the basic installation steps to deploy one or more HA K8s Clusters on AWS, in part 2 we’ll deploy some apps via [Helm Pack](https://helm.sh/) to our Kubernetes Cluster(s).

---

**NEXT**<br/>
[Pre-Requisites](docs/pre_requisites.md)