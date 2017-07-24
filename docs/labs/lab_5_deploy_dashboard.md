# Deploy Dashboard

---

You can install the Kubernetes Dashboard v1.6.1 from the Addons using:

$ kubectl config use-context kubernauts.k8s.local #switch back your context

$ kubectl create -f https://raw.githubusercontent.com/kubernetes/kops/master/addons/kubernetes-dashboard/v1.6.1.yaml

$ kubectl get pods --all-namespaces | grep dashboard
kube-system   kubernetes-dashboard-525748159-v155t 1/1       Running   0       21h
Note: the dashboard is installed in a pod as a container in the kube-system namespace.
You can find the master API URL and the admin password with:


$ kubectl config view --minify

And access the dashboard with something like this (append “ui” at the end of your api url):

https://api-kubernauts-k8s-local-xxxxxxxxxxxxxxx.eu-central-1.elb.amazonaws.com/ui

Now you may ask yourself, what can I do with my Kubernetes cluster, how can I use and deploy existing apps or build my own apps in containers and deploy them to Kubernetes?


Tip: it’s highly recommended to go through this great guide “Kubernetes by Example” by Michael Hausenblas and try all examples with your kops cluster (or your local minikube or minishift installation).


---

**NEXT**<br/>
[Create Additional Clusters](lab_6_create_additional_clusters.md)<br/><br/>
**PREVIOUS**<br/>
[Create First Cluster](lab_4_create_first_cluster.md)