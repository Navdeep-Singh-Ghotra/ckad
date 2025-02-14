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

| Item | Description | Weight |
| --- | --- | -- |
| Application Design and Build20 | Define, build and modify container imagesChoose and use the right workload resource (Deployment, DaemonSet, CronJob, etc.)Understand multi-container Pod design patterns (e.g. sidecar, init and others)Utilize persistent and ephemeral volumes | 20 |
| Application Deployment | Use Kubernetes primitives to implement common deployment strategies (e.g. blue/green or canary)Understand Deployments and how to perform rolling updatesUse the Helm package manager to deploy existing packagesKustomize| 20 |
| Application Observability and Maintenance | Understand API deprecationsImplement probes and health checksUse built-in CLI tools to monitor Kubernetes applicationsUtilize container logsDebugging in Kubernetes | 15 |
| Application Environment, Configuration and Security | Discover and use resources that extend Kubernetes (CRD, Operators)Understand authentication, authorization and admission controlUnderstand requests, limits, quotasUnderstand ConfigMapsDefine resource requirementsCreate & consume SecretsUnderstand ServiceAccountsUnderstand Application Security (SecurityContexts, Capabilities, etc.) | 25 |
| Services and Networking | Demonstrate basic understanding of NetworkPoliciesProvide and troubleshoot access to applications via servicesUse Ingress rules to expose applications | 20 |







