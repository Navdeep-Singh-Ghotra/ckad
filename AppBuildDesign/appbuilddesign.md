## Application Design and Build
- Define, build and modify container images
- Choose and use the right workload resource (Deployment, DaemonSet, CronJob, etc.)
- Understand multi-container Pod design patterns (e.g. sidecar, init and others)
- Utilize persistent and ephemeral volumes

#### Define, build and modify container images


###### 1. Navigate to the directory AppBuildDesign/TestFiles/app. Inspect the Dockerfile. Build the container image from the Dockerfile with the tag ckad-app:1.0.0. Run a container with the container image. Make the application available on port 1025. Execute a curl or wget command against the application’s endpoint.
<details>
<summary> Solution</summary>
Answer :

```ls```

```
Dockerfile  package.json  spec  src
```
```podman build -t ckad-app:1.0.0 .
podman image ls
podman run -d -p 1025:3000 7c01bebf22d2(imageID)
podman container ls
wget -O- localhost:1025
podman logs ac8fec488aba(conatinerID)
```

put answer here
</details>

###### 2. Modify the Dockerfile from the previous exercise. Change the base image to the tag 20.4-alpine and the working directory to /node. Build the container image from the Dockerfile with the tag nodejs-hello-world:1.1.0. Ensure that container image has been created by listing it.
<details>
<summary> Solution</summary>
#### Answer :

put answer here

</details>


###### 3. Pull the container image alpine:3.18.2 available on Docker Hub. Save the container image to the file alpine-3.18.2.tar. Delete the container image. Verify the container image is not listable anymore. Reinstate the container image from the file alpine-3.18.2.tar. Verify that the container image can be listed.</summary>

<details>
<summary> Solution</summary>
#### Answer :

put answer here
```YAML
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  labels:
    run: busybox
  name: busybox
spec:
  containers:
  - command:
    - env
    image: busybox
    name: busybox
    resources: {}
  dnsPolicy: ClusterFirst
  restartPolicy: Always
status: {}
```
</details>

