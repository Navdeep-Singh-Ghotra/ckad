## Application Design and Build
- Define, build and modify container images
- Choose and use the right workload resource (Deployment, DaemonSet, CronJob, etc.)
- Understand multi-container Pod design patterns (e.g. sidecar, init and others)
- Utilize persistent and ephemeral volumes

#### Define, build and modify container images


###### 1. Navigate to the directory AppBuildDesign/TestFiles/app. Inspect the Dockerfile. Build the container image from the Dockerfile with the tag ckad-app:1.0.0. Run a container with the container image. Make the application available on port 1025. Execute a curl or wget command against the application’s endpoint.
<details>
<summary> Solution</summary>

```ls```

```
Dockerfile  package.json  spec  src
podman build -t ckad-app:1.0.0 .
podman image ls
podman run -d -p 1025:3000 7c01bebf22d2(imageID)
podman container ls
wget -O- localhost:1025
podman logs ac8fec488aba(conatinerID)
```
</details>

###### 2. Modify the Dockerfile from the previous exercise. Change the base image to the tag node:current-alpine3.20. Build the container image from the Dockerfile with the tag ckad-app:1.0.1. Ensure that container image has been created by listing it.
<details>
<summary> Solution</summary>

```
podman build -t ckad-app:1.0.1 -f TestFiles/app/Dockerfile
podman image ls
podman run -d -p 1025:3000 a110590ab55a(imageID)
podman container ls
wget -O- localhost:1025
podman logs eaa8bcb25c0a(conatinerID) 

```
</details>


###### 3. Pull the container image alpine:3.18.2 available on Docker Hub. Save the container image to the file alpine-3.18.2.tar. Delete the container image. Verify the container image is not listable anymore. Reinstate the container image from the file alpine-3.18.2.tar. Verify that the container image can be listed.</summary>

<details>
<summary> Solution</summary>

```
podman pull alpine:3.18.2
podman image ls
podman image save --quiet -o myimage.tar imageID
podman rmi imageID
podman image ls
podman image load -i alpine-3.18.2.tar
```
</details>

###### Create a new Pod named nginx running the image nginx:1.17.10. Expose the container port 80. The Pod should live in the namespace named ckad. Get the details of the Pod including its IP address. Create a temporary Pod that uses the busybox:1.36.1 image to execute a wget command inside of the container. The wget command should access the endpoint exposed by the nginx container. You should see the HTML response body rendered in the terminal. Get the logs of the nginx container. Add the environment variables DB_URL=postgresql://mydb:5432 and DB_USERNAME=admin to the container of the nginx Pod. Open a shell for the nginx container and inspect the contents of the current directory ls -l. Exit out of the container.

<details>
<summary> Solution</summary>

</details>












###### 

<details>
<summary> Solution</summary>

</details>

