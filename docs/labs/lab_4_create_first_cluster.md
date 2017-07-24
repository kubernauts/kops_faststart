# Create First Cluster

---

Now that AWS is configured we are ready to create our first Kubernetes cluster.

---

Cost note: by running the next command you’ll get charged for 3 instances (1 x m3.medium and 2 x t2.medium, the cost should be less than $1 for an hour). But you can use also the free tier, please see below.

Run the following command and provide you desired zone:

$ kops create cluster --name ${NAME} --state ${KOPS_STATE_STORE} --zones eu-central-1a --yes


….
Kops has set your kubectl context to kubernauts.k8s.local

Cluster is starting.  It should be ready in a few minutes.

Suggestions:
 * validate cluster: kops validate cluster
 * list nodes: kubectl get nodes --show-labels
 * ssh to the master: ssh -i ~/.ssh/id_rsa admin@api.k8s.local
The admin user is specific to Debian. If not using Debian please use the appropriate user based on your OS.
 * read about installing addons: https://github.com/kubernetes/kops/blob/master/docs/addons.md

Verify if your master and worker nodes are running:

$ kubectl get nodes
NAME                                             STATUS    AGE       VERSION
ip-172-20-32-83.eu-central-1.compute.internal    Ready     23m       v1.6.2
ip-172-20-40-197.eu-central-1.compute.internal   Ready     1m        v1.6.2
ip-172-20-41-222.eu-central-1.compute.internal   Ready     22m       v1.6.2

Retrieve the cluster info:

$ kubectl cluster-info

Kubernetes master is running at https://api-k8s-local...
KubeDNS is running at https://api-k8s-...
….

Navigate in AWS Console in IAM under User, select the kops user and set a password for the kops user under the “Security credentials” tab:

https://console.aws.amazon.com/iam/home#/users/kops?section=security_credentials

Under the “Security credentials” tab you’ll find the console login link of the kops user and should be able to login, choose your region, find the public ip address of the master and try to ssh into the master via:

$ ssh -i .ssh/id_rsa admin@<public ip of the master>
…..
Debian GNU/Linux comes with ABSOLUTELY NO WARRANTY, to the extent
permitted by applicable law.

And verify your kubectl version:

$ kubectl version

You’re now running Kubernetes 1.6.2 cluster with a single master and two worker nodes. The master is in an Auto Scaling group and the worker nodes are in a separate group.

---

**NEXT**<br/>
[Deploy Dashboard](lab_5_deploy_dashboard.md)<br/><br/>
**PREVIOUS**<br/>
[Configure AWS](lab_3_configure_aws.md)