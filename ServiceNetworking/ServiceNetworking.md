## Services and Networking
- Demonstrate basic understanding of NetworkPolicies
- Provide and troubleshoot access to applications via services 
- Use Ingress rules to expose applications

#### Services and Networking

###### 1. Create a Service named myapp of type ClusterIP that exposes port 80 and maps to the target port 80. Create a Deployment named myapp that creates 1 replica running the image nginx:1.23.4-alpine. Expose the container port 80. Scale the Deployment to 2 replicas. Create a temporary Pod using the image busybox:1.36.1 and execute a wget command against the IP of the service. Change the service type to NodePort so that the Pods can be reached from outside of the cluster. Execute a wget command against the service from outside of the cluster.
<details>
<summary> Solution</summary>

```

```
</details>

###### 2. Kate is a developer in charge of implementing a web-based application stack. She is not familiar with Kubernetes, and asked if you could help out. The relevant objects have been created; however, connection to the application cannot be established from within the cluster. Help Kate with fixing the configuration of her YAML manifests. Navigate to the directory app-a/ch21/troubleshooting of the checked-out GitHub repository bmuschko/ckad-study-guide. Create the objects from the YAML manifest setup.yaml. Inspect the objects in the namespace y72. Create a temporary Pod using the image busybox:1.36.1 in the namespace y72. The container command should make a wget call to the Service web-app. The wget call will not be able to establish a successful connection to the Service. Identify the root cause for the connection issue and fix it. Verify the correct behavior by repeating the previous step. The wget call should return a successful response.
<details>
<summary> Solution</summary>

```

```
</details>

###### 3. Create a new Deployment named web that controls a single replica running the image bmuschko/nodejs-hello-world:1.0.0 on port 3000. Expose the Deployment with a Service named web of type ClusterIP. The Service routes traffic to the Pods controlled by the Deployment web. Make a request to the endpoint of the application on the context path /. You should see the message “Hello World.” Create an Ingress that exposes the path / for the host hello-world.exposed. The traffic should be routed to the Service created earlier. List the Ingress object. Add an entry in /etc/hosts that maps the load balancer IP address to the host hello-world.exposed. Make a request to http://hello-world.exposed. You should see the message “Hello World.”
<details>
<summary> Solution</summary>

```

```
</details>

###### 4. Any application has been exposed by an Ingress. Some of your end users report an issue with connecting to the application from outside of the cluster. Inspect the existing setup and fix the problem for your end users. Navigate to the directory app-a/ch22/troubleshooting of the checked-out GitHub repository bmuschko/ckad-study-guide. Create the objects from the YAML manifest setup.yaml. Inspect the objects in the namespace s96. Create an entry in /etc/hosts for the hostname faulty.ingress.com. Perform a HTTP call to faulty.ingress.com/ using wget or curl. Inspect the connection error. Change the configuration to ensure that end users can connect to the Ingress. Verify proper connectivity by performing another HTTP call.
<details>
<summary> Solution</summary>

```

```
</details>

###### 5. You have been tasked with setting up a network policy for an existing application stack that consists of a frontend Pod in the namespace end-user and a backend Pod in the namespace internal. Navigate to the directory app-a/ch23/app-stack of the checked-out GitHub repository bmuschko/ckad-study-guide. Create the objects from the YAML manifest setup.yaml. Inspect the objects in both namespaces. Create a network policy named app-stack in the end-user namespace. Allow egress traffic only from the frontend Pod to the backend Pod. The backend Pod should be reachable only on port 80.
<details>
<summary> Solution</summary>

```

```
</details>

###### 6. Navigate to the directory app-a/ch23/troubleshooting of the checked-out GitHub repository bmuschko/ckad-study-guide. Create the objects from the YAML manifest setup.yaml. Inspect the objects in the namespace k1 and k2. Determine the virtual IP address of Pod nginx in namespace k2. Try to make a wget call on port 80 from the Pod busybox in namespace k1 to the Pod nginx in namespace k2. The call will fail with the current setup. Create a network policy that allows performing ingress calls for all Pods in namespace k1 to the Pod nginx in namespace k2. Pods in all other namespaces should be denied to make ingress calls to Pods in namespace k2. Verify that a network connection can be established.

<details>
<summary> Solution</summary>

```

```
</details>
