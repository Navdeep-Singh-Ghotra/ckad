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
| Application Design and Build20 | 1. Define, build and modify container **images** 2. Choose and use the right workload resource (Deployment, DaemonSet, CronJob, etc.) 3. Understand multi-container Pod design patterns (e.g. sidecar, init and others) 4. Utilize persistent and ephemeral **volumes** | 20 |
| Application Deployment | 1. Use Kubernetes primitives to implement common deployment strategies (e.g. blue/green or canary) 2. Understand Deployments and how to perform rolling updates 3. Use the **Helm** package manager to deploy existing packages 4. Kustomize| 20 |
| Application Observability and Maintenance | 1. Understand API deprecations 2. Implement probes and health checks 3. Use built-in CLI tools to monitor Kubernetes applications 4. Utilize container logs 5. Debugging in Kubernetes | 15 |
| Application Environment, Configuration and Security | 1. Discover and use resources that extend Kubernetes (CRD, Operators) 2. Understand authentication, authorization and admission control 3. Understand requests, limits, quotas 4.Understand ConfigMaps 5. Define resource requirements 6. Create & consume Secrets 7. Understand ServiceAccounts 8. Understand Application Security (SecurityContexts, Capabilities, etc.) | 25 |
| Services and Networking | 1. Demonstrate basic understanding of NetworkPolicies 2. Provide and troubleshoot access to applications via services 3. Use Ingress rules to expose applications | 20 |







