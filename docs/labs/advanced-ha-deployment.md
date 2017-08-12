# Advanced HA deployment

---

To create an HA deployment with 3 masters in 3 AZs, please refer to the Kops documentation and try something like this:

```
kops create cluster \
--name kubernauts2.k8s.local \
--state ${KOPS_STATE_STORE}    \
--node-count 3     \
--zones eu-central-1a,eu-central-1b,eu-central-1c     \
--master-zones eu-central-1a,eu-central-1b,eu-central-1c     \
--node-size t2.micro     \
--master-size t2.micro     \
--topology public     \
--networking calico  \
--target=terraform
```

With that the terraform model with be created under out/terraform.

Please verify your terraform version and run the following commands:

```
$ terraform version
Terraform v0.10.0

$ cd out/terraform/
$ terraform init
$ terraform plan
$ terraform apply
```

You should get the terraform output like this:

![](/assets/kops-terraform-apply.png)

In AWS Web-Console you should see 3 masters and 3 nodes running in 3 different AZs:

![](/assets/kops-aws-nodes.png)

SSH into the master and enjoy your HA'ed Kubernetes 1.7 cluster:

```
admin@ip-172-20-124-156:~$ kubectl get nodes
NAME                                              STATUS    AGE       VERSION
ip-172-20-124-156.eu-central-1.compute.internal   Ready     7m        v1.7.0
ip-172-20-47-35.eu-central-1.compute.internal     Ready     6m        v1.7.0
ip-172-20-55-110.eu-central-1.compute.internal    Ready     7m        v1.7.0
ip-172-20-70-156.eu-central-1.compute.internal    Ready     7m        v1.7.0
ip-172-20-79-160.eu-central-1.compute.internal    Ready     6m        v1.7.0
ip-172-20-98-236.eu-central-1.compute.internal    Ready     6m        v1.7.0
```



