# Kubernetes Research

Documentation -> https://kubernetes.io/docs/concepts/workloads/controllers/

## Prepare the Raspberry PIs for Kubernetes (K3S) to be installed

### Change to root
```shell
sudo su -
```
### Run the following commands to prepare the pis for K3S
```shell
sudo iptables -F bin/iptables-legacy | sudo update-alternatives --set ip6tables /usr/sbin/ip6tables-legacy
sudo update-alternatives --set iptables /usr/sbin/iptables-legacy
sudo update-alternatives --set ip6tables /usr/sbin/ip6tables-legacy
reboot
```

### Install K3S (Light version of Kubernetes) in the Master Node.
```shell
curl -sfl https://get.k3s.io | K3S_KUBECONFIG_MODE="644" sh -s
```

### Get all the nodes in Kubernetes
```shell
kubectl get nodes
```

### Get the token to register the rest of the nodes to the Master Node:
```shell
cat /var/lib/rancher/k3s/server/node-token
```
### Nodes Command to install K3S and register the Worker Nodes to the Master Node
```shell
curl -sfL https://get.k3s.io | K3S_TOKEN="[token from previous step]" K3S_URL="https://[MASTER NODE IP]:6443" K3S_NODE_NAME="[NODE NAME]" sh -
```

### Deploy Apps to the Nodes, using a manifest file:
```shell
kubectl apply -f [name of the file].yaml
```

### Will show you the pods/containes deployed in your nodes
```shell
kubectl get pods
```

### Will show you the pods and in which node they are deployed.
```shell
kubectl get pods -o wide
```

### To expose your application to the outside network, you will need to create another manifest file
TODO

### View the services that are running and exposed to the network
```shell
kubectl get services
```


# Rancher Install
### In a separate node with Ubuntu version 18 or greater, do the following:
```shell
mkdir /etc/rancher/rke2
touch config.yaml
```

### Add to the config file
```yaml
token: myrancher
tls-san:
 - 192.168.50.109
```

### Then download Rancher
```shell
curl -sfL https://get.rancher.io | sh -
```



