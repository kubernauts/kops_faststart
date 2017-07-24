# Create Additional Clusters

---

There are many different configurations of a Kops cluster.

---

Run a second cluster with one master and 3 nodes in 3 AZs.

```
$ kops create cluster --name kubernauts1.k8s.local --node-count 3 --state ${KOPS_STATE_STORE} --zones eu-central-1a,eu-central-1b,eu-central-1c --yes
```

It is also possible to create a cluster to use the free tier with t2.micro instances.

```
$ kops create cluster --name kubernauts2.k8s.local --state ${KOPS_STATE_STORE} --zones eu-central-1a --node-count=2 --node-size=t2.micro --master-size=t2.micro
```

**Note**<br/>
In the previous example we did not specify `--yes`.  This means that the changes have not been applied.  

Apply the changes by updating the cluster.

```
$ kops update cluster kubernauts2.k8s.local --state ${KOPS_STATE_STORE} --yes
```

You can now see your new free tier nodes.

```
$ kubectl get nodes
NAME                                             STATUS    AGE       VERSION
ip-172-20-42-198.eu-central-1.compute.internal   Ready     3m        v1.6.2
ip-172-20-51-199.eu-central-1.compute.internal   Ready     6m        v1.6.2
ip-172-20-56-194.eu-central-1.compute.internal   Ready     3m        v1.6.2
```

To use your first cluster you need to switch the `kubectl` context to the first cluster.

```
$ kubectl config set-context kubernauts1.k8s.local
$ kubectl config use-context kubernauts1.k8s.local
```

Delete both Clusters

```
$ kops delete cluster kubernauts1.k8s.local --state=${KOPS_STATE_STORE} --yes
$ kops delete cluster kubernauts2.k8s.local --state=${KOPS_STATE_STORE} --yes
```

---

**NEXT**<br/>
[Wrap Up](wrap_up.md)<br/><br/>
**PREVIOUS**<br/>
[Deploy Dashboard](lab_5_deploy_dashboard.md)