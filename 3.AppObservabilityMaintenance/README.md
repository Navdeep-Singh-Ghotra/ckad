## Application Observability and Maintenance 15 %
- Understand API deprecations  
- Implement probes and health checks
- Use built-in CLI tools to monitor Kubernetes applications
- Utilize container logs
- Debugging in Kubernetes

#### Application deployment


###### 1. The Kubernetes administrator in charge of the cluster is planning to upgrade all nodes from Kubernetes 1.8 to 1.28. You defined multiple Kubernetes YAML manifests that operate an application stack. The administrator provided you with a Kubernetes 1.28 test environment. Make sure that all YAML manifests are compatible with Kubernetes version 1.28. Navigate to the directory app-a/ch13/deprecated of the checked-out GitHub repository bmuschko/ckad-study-guide. Inspect the files deployment.yaml and configmap.yaml in the current directory. Create the objects from the YAML manifests. Modify the definitions as needed. Verify that the objects can be instantiated with Kubernetes 1.28.
<details>
<summary> Solution</summary>

```

```
</details>

###### 2. Define a new Pod named web-server with the image nginx:1.23.0 in a YAML manifest. Expose the container port 80. Do not create the Pod yet.For the container, declare a startup probe of type httpGet. Verify that the kubelet can make a request to the root context endpoint. Use the default configuration for the probe.For the container, declare a readiness probe of type httpGet.Verify that the kubelet can make a request to the root context endpoint. Wait five seconds before checking for the first time.For the container, declare a liveness probe of type httpGet. Verify that the kubelet can make a request to the root context endpoint. Wait 10 seconds before checking for the first time. The probe should run the check every 30 seconds.Create the Pod and follow the life cycle phases of the Pod during the process.Inspect the runtime details of the Pod’s probes.
<details>
<summary> Solution</summary>

```

```
</details>

###### 3. In this exercise, you will practice your troubleshooting skills by inspecting a misconfigured Pod. Navigate to the directory app-a/ch15/troubleshooting of the checked-out GitHub repository bmuschko/ckad-study-guide. Create a new Pod from the YAML manifest in the file pod.yaml. Check the Pod’s status. Do you see any issue? Render the logs of the running container and identify an issue. Shell into the container. Can you verify the issue based on the rendered log message? Suggest solutions that can fix the root cause of the issue.
<details>
<summary> Solution</summary>

```

```
</details>

###### 4. You will inspect the metrics collected by the metrics server. Navigate to the directory app-a/ch15/stress-test of the checked-out GitHub repository bmuschko/ckad-study-guide. The current directory contains the YAML manifests for three Pods, stress-1-pod.yaml, stress-2-pod.yaml, and stress-3-pod.yaml. Inspect those manifest files. Create the namespace stress-test and the Pods inside of the namespace. Use the data available through the metrics server to identify which of the Pods consumes the most memory. Prerequisite: You will need to install the metrics server if you want to be able to inspect actual resource metrics. You can find installation instructions on the project’s GitHub page.
<details>
<summary> Solution</summary>

```

```
</details>
