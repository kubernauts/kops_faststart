# Install Kops

---

To create, configure and destroy Kubernetes clusters on AWS the `kops` command is used.

---

## Install

**On Mac**

On Mac the easiest way is to install kops is via the [Brew](https://brew.sh) package manager.

```
$ brew update && brew install kops
```

**On Linux**

On Linux the latest release 1.6.2 is available under:
https://github.com/kubernetes/kops/releases/tag/1.6.2

```
$ wget https://github.com/kubernetes/kops/releases/download/1.6.2/kops-linux-amd64

$ chmod +x kops-linux-amd64                 # Add execution permissions
$ mv kops-linux-amd64 /usr/local/bin/kops   # Move the kops to /usr/local/bin
```

**On Windows**

On Windows install Ubuntu / CentOS with Vagrant and then use the previous Linux instructions.

Confirm the version of `kops`.

```
$ kops version
Version 1.6.2
```

---

**NEXT**<br/>
[Install Kubectl](lab_2_install_kubectl.md)<br/><br/>
**PREVIOUS**<br/>
[Pre-Requisites](/docs/pre_requisites.md)