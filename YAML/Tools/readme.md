### Install RKE

```
curl -s https://api.github.com/repos/rancher/rke/releases/latest | grep download_url | grep amd64 | cut -d '"' -f 4 | wget -qi -
chmod +x rke_linux-amd64
sudo mv rke_linux-amd64 /usr/local/bin/rke
rke --version
```

### Install Kubectl

```
curl -LO https://storage.googleapis.com/kubernetes-release/release/`curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt`/bin/linux/amd64/kubectl
chmod +x ./kubectl
sudo mv ./kubectl /usr/local/bin/kubectl
kubectl version --client
```

### Install Helm

```
curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3
chmod 700 get_helm.sh
./get_helm.sh
```

### Install container runtime in the VMs

```
sudo apt-get update -y
sudo apt-get install -y apt-transport-https ca-certificates curl software-properties-common
curl https://releases.rancher.com/install-docker/20.10.sh | sh
modprobe br_netfilter
sysctl net.bridge.bridge-nf-call-iptables=1
sudo systemctl enable docker
sudo usermod -aG docker $USER


## Step 3: Create Cluster

Get the k8s versions available

```

rke config --list-version --all

```
export KUBECONFIG= $(pwd)/kube_config_cluster.yaml
```

## Check certs

cd /etc/kubernetes/ssl/

rke cert rotate --config 1-create-cluster/cluster.yaml

##### Create an ssh keypair on the host machine

```
ssh-keygen -t rsa -b 2048
```

##### Copy SSH Keys to all the kubernetes nodes

The root password is **kubeadmin**

```
ssh-copy-id root@172.16.16.101
ssh-copy-id root@172.16.16.102
```

## Prepare the kubernetes nodes (node1, node2)

##### Disable Firewall

```
ufw disable
```

##### Disable swap

```
swapoff -a; sed -i '/swap/d' /etc/fstab
```
