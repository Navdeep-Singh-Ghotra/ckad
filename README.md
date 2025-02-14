# ckad
Contains practice questions for CKAD

# Install minikube instructions
```bash
minikube start --kubernetes-version=1.31.6 -p navdeepcluster addons enable metrics-server
```

# install kubectl
```
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl.sha256"
echo "$(cat kubectl.sha256)  kubectl" | sha256sum --check
sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
```
# install kustomize
```
put commands here
```

# test command 

```
alais k=kubectl
k version
```
Out put must be something like

```
Client Version: v1.31.6
Kustomize Version: v5.4.2
Server Version: v1.31.6
```




