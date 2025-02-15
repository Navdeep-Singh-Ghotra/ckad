## Application Deployment 20%
- Use Kubernetes primitives to implement common deployment strategies (e.g. blue/green or canary) 
- Understand Deployments and how to perform rolling updates
- Use the Helm package manager to deploy existing packages
- Kustomize

#### Application deployment


###### 1. Create a Deployment named nginx with 3 replicas. The Pods should use the nginx:1.23.0 image and the name nginx. The Deployment uses the label tier=backend. The Pod template should use the label app=v1. List the Deployment and ensure that the correct number of replicas is running. Update the image to nginx:1.23.4. Verify that the change has been rolled out to all replicas. Assign the change cause “Pick up patch version” to the revision. Scale the Deployment to 5 replicas. Have a look at the Deployment rollout history. Revert the Deployment to revision 1. Ensure that the Pods use the image nginx:1.23.0.
<details>
<summary> Solution</summary>

```

```
</details>

###### 2. Create a Deployment named nginx with 1 replica. The Pod template of the Deployment should use container image nginx:1.23.4; set the CPU resource request to 0.5 and the memory resource request/limit to 500Mi. Create a HorizontalPodAutoscaler for the Deployment named nginx-hpa that scales to a minimum of 3 and a maximum of 8 replicas. Scaling should happen based on an average CPU utilization of 75% and an average memory utilization of 60%. Inspect the HorizontalPodAutoscaler object and identify the currently-utilized resources. How many replicas do you expect to exist?
<details>
<summary> Solution</summary>

```

```
</details>

###### 3. One of your teammates created a Deployment YAML manifest to operate the container image grafana/grafana:9.5.9. Create the Deployment object from the YAML manifest file deployment-grafana.yaml:
```YAML
apiVersion: apps/v1
kind: Deployment
metadata:
  name: grafana
spec:
  replicas: 6
  selector:
    matchLabels:
      app: grafana
  template:
    metadata:
      labels:
        app: grafana
    spec:
      containers:
      - image: grafana/grafana:9.5.9
        name: grafana
        ports:
        - containerPort: 3000
```
###### You need to update all replicas with the container image grafana/grafana:10.1.2. Make sure that the rollout happens in batches of two replicas at a time. Ensure that a readiness probe is defined.
<details>
<summary> Solution</summary>

```

```
</details>

###### 4. In this exercise, you will set up a blue-green Deployment scenario. You’ll first create the initial (blue) Deployment and expose it with a Service. Later, you will create a second (green) Deployment and switch over traffic.Create a Deployment named nginx-blue with 3 replicas. The Pod template of the Deployment should use container image nginx:1.23.0 and assign the label version=blue. Expose the Deployment with a Service of type ClusterIP named nginx. Map the incoming and outgoing port to 80. Select the Pod with label version=blue. Run a temporary Pod with the container image alpine/curl:3.14 to make a call against the Service using curl. Create a second Deployment named nginx-green with 3 replicas. The Pod template of the Deployment should use container image nginx:1.23.4 and assign the label version=green. Change the Service’s label selection so that traffic will be routed to the Pods controlled by the Deployment nginx-green. Delete the Deployment named nginx-blue. Run a temporary Pod with the container image alpine/curl:3.14 to make a call against the Service.
<details>
<summary> Solution</summary>

```

```
</details>

###### 5. In this exercise, you will use Helm to install Kubernetes objects needed for the open source monitoring solution Prometheus. The easiest way to install Prometheus on top of Kubernetes is with the help of the prometheus-operator Helm chart. You can search for the kube-prometheus-stack on Artifact Hub. Add the repository to the list of known repositories accessible by Helm with the name prometheus-community. Update to the latest information about charts from the respective chart repository. Run the Helm command for listing available Helm charts and their versions. Identify the latest chart version for kube-prometheus-stack. Install the the chart kube-prometheus-stack. List the installed Helm chart. List the Service named prometheus-operated created by the Helm chart. The object resides in the default namespace. Use the kubectl port-forward command to forward the local port 8080 to the port 9090 of the Service. Open a browser and bring up the Prometheus dashboard. Stop port forwarding and uninstall the Helm chart.
<details>
<summary> Solution</summary>

```

```
</details>