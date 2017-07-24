# Deploy Dashboard

---

The Dashboard allows you to manage a Kubernetes cluster using a web UI.

---

You can now install the Kubernetes Dashboard v1.6.1 from the Kubernetes Addons.

```
$ kubectl create -f https://raw.githubusercontent.com/kubernetes/kops/master/addons/kubernetes-dashboard/v1.6.1.yaml
$ kubectl -n kube-system get po,svc -l k8s-app=kubernetes-dashboard
NAME                                      READY     STATUS    RESTARTS   AGE
po/kubernetes-dashboard-525748159-kl453   1/1       Running   0          2m

NAME                       CLUSTER-IP      EXTERNAL-IP   PORT(S)   AGE
svc/kubernetes-dashboard   100.64.31.154   <none>        80/TCP    2m
```

**Note**<br/>
The Dashboard is installed in a pod in the `kube-system` namespace.

Get the Master API URL and the admin users password.

```
$ kubectl config view --minify
apiVersion: v1
clusters:
- cluster:
    certificate-authority-data: REDACTED
    server: https://api-kubernauts-k8s-local-xxxxxxxxxxxxxxx.eu-central-1.elb.amazonaws.com  <--
  name: kubernauts.k8s.local
contexts:
- context:
    cluster: kubernauts.k8s.local
    user: kubernauts.k8s.local
  name: kubernauts.k8s.local
current-context: kubernauts.k8s.local
kind: Config
preferences: {}
users:
- name: kubernauts.k8s.local
  user:
    client-certificate-data: REDACTED
    client-key-data: REDACTED
    password: XXXXXXXXXXXXXXXXXXXXXXXX  <--
    username: admin
```

Then access the dashboard by appending `/ui/` to end of the Master server API URL.  Login with the admin user.

https://api-kubernauts-k8s-local-xxxxxxxxxxxxxxx.eu-central-1.elb.amazonaws.com/ui

Now you may ask yourself, what can I do with my Kubernetes cluster, how can I use it to deploy existing apps or build my own apps in containers and deploy them to Kubernetes?

**Tip**<br/>
It is highly recommended to go through this great guide "[Kubernetes by Example](http://kubernetesbyexample.com)" by [Michael Hausenblas](https://twitter.com/mhausenblas) and try all examples with your kops cluster (or your local minikube or minishift installation).

---

**NEXT**<br/>
[Create Additional Clusters](lab_6_create_additional_clusters.md)<br/><br/>
**PREVIOUS**<br/>
[Create First Cluster](lab_4_create_first_cluster.md)