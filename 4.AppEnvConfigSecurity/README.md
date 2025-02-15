## Application Environment, Configuration and Security
- Discover and use resources that extend Kubernetes (CRD, Operators)
- Understand authentication, authorization and admission control
- Understand requests, limits, quotas 
- Understand ConfigMaps 
- Define resource requirements
- Create & consume Secrets
- Understand ServiceAccounts
- Understand Application Security (SecurityContexts, Capabilities, etc.)

#### Application Environment, Configuration and Security

###### 1. You decide to manage a MongoDB installation in Kubernetes with the help of the official community operator. This operator provides a CRD. After installing the operator, you will interact with the CRD.Navigate to the directory app-a/ch16/mongodb-operator of the checked-out GitHub repository bmuschko/ckad-study-guide. Install the operator using the following command: kubectl apply -f mongodbcommunity.mongodb.com_mongodb​community.yaml. List all CRDs using the appropriate kubectl command. Can you identify the CRD that was installed by the installation procedure? Inspect the schema of the CRD. What are the type and property names of this CRD?
<details>
<summary> Solution</summary>

```

```
</details>

###### 2. As an application developer, you may want to install Kubernetes functionality that extends the platform using the Kubernetes operator pattern. The objective of this exercise is to familiarize yourself with creating and managing CRDs. You will not need to write a controller.Create a CRD resource named backup.example.com with the following specifications: 
```
Group: example.com
Version: v1
Kind: Backup
Singular: backup
Plural: backups
Properties of type string: cronExpression, podName, path
```
###### Retrieve the details for the Backup custom resource created in the previous step. Create a custom object named nginx-backup for the CRD. Provide the following property values:
```
cronExpression: 0 0 * * * 
podName: nginx 
path: /usr/local/nginx 
```
###### Retrieve the details for the nginx-backup object created in the previous step.
<details>
<summary> Solution</summary>

```

```
</details>

###### 3. The premise of this exercise is to create a new user and add her to the kubeconfig file. You will then define a context that uses the user, switch to the context, and execute a kubectl command. Create a certificate for a user named mary. Do not provide any permissions to the user. Add the user to the kubeconfig file. Define the context named mary-context that assigns the user to a cluster already available in the kubeconfig file. Set the currently selected context to mary-context. Create a Pod using kubectl. What result do you expect to see?
<details>
<summary> Solution</summary>

```

```
</details>

###### 4. You will use RBAC to grant permissions to a service account. The permissions should apply only to certain API resources and operations.Create a new namespace named t23. Create a Pod named service-list in the namespace t23. The container uses the image alpine/curl:3.14 and makes a curl call to the Kubernetes API that lists Service objects in the default namespace in an infinite loop. Create and attach the service account api-call to the Pod. Inspect the container logs after the Pod has been started. What response do you expect to see from the curl command? Assign a ClusterRole and RoleBinding to the service account that allows only the operation needed by the Pod. Note the response from the curl command.
<details>
<summary> Solution</summary>

```

```
</details>

###### 5. Identify the admission controller plugins that have been configured for the API server. Locate the configuration file of the API server. Inspect the command-line flag that defines the admission controller plugins. Capture the value.
<details>
<summary> Solution</summary>

```

```
</details>

###### 6. You have been tasked with creating a Pod for running an application in a container. During application development, you ran a load test for figuring out the minimum amount of resources needed and the maximum amount of resources the application is allowed to grow to. Define those resource requests and limits for the Pod.Define a Pod named hello-world running the container image bmuschko/nodejs-hello-world:1.0.0. The container exposes the port 3000. Add a Volume of type emptyDir and mount it in the container path /var/log. For the container, specify the following minimum number of resources: CPU: 100m Memory: 500Mi Ephemeral storage: 1Gi For the container, specify the following maximum number of resources: Memory: 500Mi Ephemeral storage: 2Gi Create the Pod from the YAML manifest. Inspect the Pod details. Which node does the Pod run on?
<details>
<summary> Solution</summary>

```

```
</details>

###### 7. In this exercise, you will create a resource quota with specific CPU and memory limits for a new namespace. Pods created in the namespace will have to adhere to those limits. Create a ResourceQuota named app under the namespace rq-demo using the following YAML definition in the file resourcequota.yaml:
```YAML
apiVersion: v1
kind: ResourceQuota
metadata:
  name: app
spec:
  hard:
    pods: "2"
    requests.cpu: "2"
    requests.memory: 500Mi
```
###### Create a new Pod that exceeds the limits of the resource quota requirements, e.g., by defining 1Gi of memory but stays below the CPU, e.g., 0.5. Write down the error message. Change the request limits to fulfill the requirements to ensure that the Pod can be created successfully. Write down the output of the command that renders the used amount of resources for the namespace.
<details>
<summary> Solution</summary>

```

```
</details>

###### 8. A LimitRange can restrict resource consumption for Pods in a namespace, and assign default computing resources if no resource requirements have been defined. You will practice the effects of a LimitRange on the creation of a Pod in different scenarios. Navigate to the directory app-a/ch18/limitrange of the checked-out GitHub repository bmuschko/ckad-study-guide. Inspect the YAML manifest definition in the file setup.yaml. Create the objects from the YAML manifest file. Create a new Pod named pod-without-resource-requirements in the namespace d92 that uses the container image nginx:1.23.4-alpine without any resource requirements. Inspect the Pod details. What resource definitions do you expect to be assigned? Create a new Pod named pod-with-more-cpu-resource-requirements in the namespace d92 that uses the container image nginx:1.23.4-alpine with a CPU resource request of 400m and limits of 1.5. What runtime behavior do you expect to see? Create a new Pod named pod-with-less-cpu-resource-requirements in the namespace d92 that uses the container image nginx:1.23.4-alpine with a CPU resource request of 350m and limits of 400m. What runtime behavior do you expect to see?
<details>
<summary> Solution</summary>

```

```
</details>

###### 9. In this exercise, you will first create a ConfigMap from a YAML configuration file as a source. Later, you’ll create a Pod, consume the ConfigMap as Volume, and inspect the key-value pairs as files. Navigate to the directory app-a/ch19/configmap of the checked-out GitHub repository bmuschko/ckad-study-guide. Inspect the YAML configuration file named application.yaml. Create a new ConfigMap named app-config from that file. Create a Pod named backend that consumes the ConfigMap as Volume at the mount path /etc/config. The container runs the image nginx:1.23.4-alpine. Shell into the Pod and inspect the file at the mounted Volume path.
<details>
<summary> Solution</summary>

```

```
</details>

###### 10. You will first create a Secret from literal values in this exercise. Next, you’ll create a Pod and consume the Secret as environment variables. Finally, you’ll print out its values from within the container. Create a new Secret named db-credentials with the key/value pair db-password=passwd. Create a Pod named backend that uses the Secret as an environment variable named DB_PASSWORD and runs the container with the image nginx:1.23.4-alpine.Shell into the Pod and print out the created environment variables. You should be able to find the DB_PASSWORD variable.
<details>
<summary> Solution</summary>

```

```
</details>

###### 11. Define a Pod named busybox-security-context that uses the image busybox:1.36.1 for a single container running the command sh -c sleep 1h. Add an ephemeral Volume of type emptyDir. Mount the Volume to the container at /data/test. Define a security context that runs the container with user ID 1000, with group ID 3000, and the filesystem group ID 2000. Ensure that the container should not allow privilege escalation. Create the Pod object and ensure that it transitions into the “Running” status. Open a shell to the running container and create a new file named logs.txt in the directory /data/test. What’s the file’s user ID and group ID?
<summary> Solution</summary>

```

```
</details>

###### 12. Create a Deployment named nginx in the namespace h20 with the 3 replicas. The Pod template should use the the image nginx:1.25.3-alpine. Using the security context, assign the drop Linux capability for that Pod template. The attribute for the drop capabilities should use the value all. Create the Deployment object and inspect its replicas. Does NGINX work as expected?
<summary> Solution</summary>

```

```
</details>







