# Install Kubectl

---

To enable management of the Kubernetes cluster the `kubectl` command is used.

---


## Install

Download the `kubectl` command.

**On Mac**
```
$ curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/darwin/amd64/kubectl
```

**On Linux**
```
$ curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl
```

Setup `kubectl` permissions and move it to the `bin/` directory.

```
$ chmod +x kubectl
$ sudo mv kubectl /usr/local/bin/
```

Confirm the version of `kubectl`.

```
$ kubectl version
Client Version: version.Info{Major:"1", Minor:"7", GitVersion:"v1.7.1",.. ", GoVersion:"go1.8.3"
```

**Note**<br>
As the Kubernetes API server is not yet deployed the `kubectl version` command will take a while to timeout before showing you the version.

To further configure `kubectl` please refer to the great documentation on the [kubernetes.io](https://kubernetes.io/docs/tasks/tools/install-kubectl/) site.


## Enable Command Completion

Enable Bash completetion for `kubectl`.

**On Mac**

If running Bash 3.2 (included with macOS).

```
$ brew install bash-completion
$ kubectl completion -h
$ source $(brew --prefix)/etc/bash_completion
```

**On Linux**
```
$ source <(kubectl completion bash)
$ echo "source <(kubectl completion bash)" >> ~/.bashrc 
```

---

**NEXT**<br/>
[Configure AWS](lab_3_configure_aws.md)<br/><br/>
**PREVIOUS**<br/>
[Install Kops](lab_1_install_kops.md)