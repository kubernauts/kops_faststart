# Deploy \(existing\) Apps with HelmPack

---

You can use [Helm](https://github.com/kubernetes/helm), the Kubernetes package installer which manages existing [Kubernetes Charts](https://github.com/kubernetes/charts) to deploy ready to use kube apps and write your own charts for your own apps.

To install Helm, please refer to the [download page](https://github.com/kubernetes/helm/releases) and install the appropriate package for your OS and refer to [Helm Quick Start guide](https://docs.helm.sh/using_helm/#quickstart-guide).

On Mac you can install Helm client and the server component “Tiller" with:

```
$ brew install kubernetes-helm

$ helm init

$ helm repo update
```

And search for existing apps, e.g. with:

```
$ helm search

NAME VERSIONDESCRIPTION

stable/acs-engine-autoscaler0.1.0 Scales worker nodes within agent pools

stable/artifactory 5.4.1 Universal Repository Manager supporting

stable/aws-cluster-autoscaler0.2.2 Scales worker nodes within autoscaling groups.  
…
```

To search for an existing app, e.g. Minio, you can do:

```
$ helm search minio
NAME            VERSION    DESCRIPTION
stable/minio    0.1.3      Distributed object storage server built for clo...
```

And you can deploy for instance Minio with:

```
$ helm install stable/minio
```

And in the Dashboard you can access the Minio Browser \(under discovery and load balancing you’ll find the link\).

To delete the app, you’ve to find the **release** name with:

```
$ helm list | grep minio
whopping-pika    1           Sun Jul 23 02:00:04 2017    DEPLOYED    minio-0.1.3            

$ helm delete whopping-pika1
```

**Note**: we recommend to refer to the [official Helm documentation](https://docs.helm.sh/) and learn more about Helm and how to [write your own Charts](https://hackernoon.com/the-missing-ci-cd-kubernetes-component-helm-package-manager-1fe002aac680) and more.

