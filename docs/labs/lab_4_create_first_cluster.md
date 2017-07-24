# Create First Cluster

---

Now that AWS is configured we are ready to create our first Kubernetes cluster.

---

**Cost note**<br/>
By running the next command you’ll get charged for 3 instances (1 x m3.medium and 2 x t2.medium, the cost should be less than $1 for an hour). But you can use also the **free tier**.

Run the following command and provide your desired zone.

```
$ kops create cluster --name ${NAME} --state ${KOPS_STATE_STORE} --zones eu-central-1a --yes
```

The Kubernetes cluster is now starting.  It should be ready in a few minutes.  Kops has also set your `kubectl` context to be `kubernauts.k8s.local`.

The following Asciicast shows the cluster being created.

<script type="text/javascript" src="https://asciinema.org/a/jPqthn65H9fQhi9iezB1gdtda.js" id="asciicast-jPqthn65H9fQhi9iezB1gdtda" async></script>

Verify if your master and worker nodes are running.

```
$ kubectl get nodes
NAME                                             STATUS    AGE       VERSION
ip-172-20-32-83.eu-central-1.compute.internal    Ready     23m       v1.6.2
ip-172-20-40-197.eu-central-1.compute.internal   Ready     1m        v1.6.2
ip-172-20-41-222.eu-central-1.compute.internal   Ready     22m       v1.6.2
```

Retrieve the cluster info.

```
$ kubectl cluster-info
Kubernetes master is running at https://api-k8s-local...
KubeDNS is running at https://api-k8s-...
```

Use the following link to open the AWS Console at the IAM service and the `kops` user summary page.

https://console.aws.amazon.com/iam/home#/users/kops?section=security_credentials

Under the *Security credentials* tab set a password for the `kops` user.  The *Console login link* for the `kops` user will then be created.  Use it to login as the `kops` user with the password you just set.  

Once you have logged in choose the region you created the cluster in and find the public ip address of the master EC2 instance.  You can now ssh into the master.

```
$ ssh -i .ssh/id_rsa admin@<public_ip_of_master>
Debian GNU/Linux comes with ABSOLUTELY NO WARRANTY, to the extent
permitted by applicable law.
```

And verify your kubectl version:

```
$ kubectl version
Client Version: version.Info{Major:"1", Minor:"6", GitVersion:"v1.6.2", GitCommit:"477efc3cbe6a7effca06bd1452fa356e2201e1ee", GitTreeState:"clean", BuildDate:"2017-04-19T20:33:11Z", GoVersion:"go1.7.5", Compiler:"gc", Platform:"linux/amd64"}
Server Version: version.Info{Major:"1", Minor:"6", GitVersion:"v1.6.2", GitCommit:"477efc3cbe6a7effca06bd1452fa356e2201e1ee", GitTreeState:"clean", BuildDate:"2017-04-19T20:22:08Z", GoVersion:"go1.7.5", Compiler:"gc", Platform:"linux/amd64"}
```

You’re now running Kubernetes 1.6.2 cluster with a single master and two worker nodes. The master is in an Auto Scaling group and the worker nodes are in a separate group.

---

**NEXT**<br/>
[Deploy Dashboard](lab_5_deploy_dashboard.md)<br/><br/>
**PREVIOUS**<br/>
[Configure AWS](lab_3_configure_aws.md)