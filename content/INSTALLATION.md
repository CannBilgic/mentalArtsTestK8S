# Kubernetes Lab Cheatsheet

## Install kubectl

```bash
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
```

```bash
sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
```

```bash
kubectl version --client --output yaml
```

```bash
clientVersion:
  buildDate: "2023-10-18T11:42:52Z"
  compiler: gc
  gitCommit: a8a1abc25cad87333840cd7d54be2efaf31a3177
  gitTreeState: clean
  gitVersion: v1.28.3
  goVersion: go1.20.10
  major: "1"
  minor: "28"
  platform: linux/amd64
kustomizeVersion: v5.0.4-0.20230601165947-6ce0bf390ce3
```

## Install Kind

Install kind via Go

```bash
wget https://go.dev/dl/go1.21.3.linux-amd64.tar.gz
rm -rf /usr/local/go && tar -C /usr/local -xzf go1.21.3.linux-amd64.tar.gz
export PATH=$PATH:/usr/local/go/bin
go version
```

```bash
go install sigs.k8s.io/kind@latest
```

Install via binary

```bash
# For AMD64 / x86_64
[ $(uname -m) = x86_64 ] && curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.20.0/kind-$(uname)-amd64
# For ARM64
[ $(uname -m) = aarch64 ] && curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.20.0/kind-$(uname)-arm64
chmod +x ./kind
sudo mv ./kind /usr/local/bin/kind
```

## Create a Cluster

```bash
kind create cluster --name mentalarts
```

```bash
Creating cluster "mentalarts" ...
 ✓ Ensuring node image (kindest/node:v1.27.3) 🖼
 ✓ Preparing nodes 📦 📦 📦 📦 
 ✓ Configuring the external load balancer ⚖️ 
 ✓ Writing configuration 📜 
 ✓ Starting control-plane 🕹️ 
 ✓ Installing CNI 🔌 
 ✓ Installing StorageClass 💾
Set kubectl context to "kind-mentalarts"
You can now use your cluster with:

kubectl cluster-info --context kind-mentalarts

Have a nice day! 👋
```

```bash
kubectl cluster-info --context kind-mentalarts
```

```bash
Kubernetes control plane is running at https://
KubeDNS is running at https://
```

```bash
kubectl get nodes
```

```bash
NAME                 STATUS   ROLES                  AGE   VERSION
mentalarts-control-plane   Ready    control-plane,master   10m   v1.22.1
```

## Building Docker Image

```bash
docker build -t mentalarts/fastapi-demo:latest .
```

## Load Image to KinD
    
```bash
kind load docker-image mentalarts/fastapi-demo:latest -n mentalarts
```
