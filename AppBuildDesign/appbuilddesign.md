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
podman image save --quiet -o alpine-3.18.2.tar imegeIDc1aabb73d233
podman rmi imageID
podman image ls
podman image load -i alpine-3.18.2.tar
```
</details>

###### 4. Create a new Pod named nginx running the image nginx:1.17.10. Expose the container port 80. The Pod should live in the namespace named ckad. Get the details of the Pod including its IP address. Create a temporary Pod that uses the busybox:1.36.1 image to execute a wget command inside of the container. The wget command should access the endpoint exposed by the nginx container. You should see the HTML response body rendered in the terminal. Get the logs of the nginx container. Add the environment variables DB_URL=postgresql://mydb:5432 and DB_USERNAME=admin to the container of the nginx Pod. Open a shell for the nginx container and inspect the contents of the current directory ls -l. Exit out of the container.

<details>
<summary> Solution</summary>

```
k get po
k get ns
default           Active   11h
kube-node-lease   Active   11h
kube-public       Active   11h
kube-system       Active   11h
mynamespace       Active   11h

k run nginx --image=nginx --namespace=ckad --port=80
Error from server (NotFound): namespaces "ckad" not found

k run nginx --image=nginx --namespace=ckad --port=80 --dry=client -op yaml > TestFiles/4/4.1.nginx-pod.yaml
bash: TestFiles/4/4.1.nginx-pod.yaml: No such file or directory
mkdir TestFiles/4
k run nginx --image=nginx --namespace=ckad --port=80 --dry-run=client -o yaml > TestFiles/4/4.1.nginx-pod.yaml
Error from server (NotFound): error when creating "TestFiles/4/4.1.nginx-pod.yaml": namespaces "ckad" not found

k create namespace ckad --dry-run=client -o yaml > TestFiles/4/4.1.namespace.yaml
k create -f TestFiles/4/4.1.namespace.yaml 
namespace/ckad created
k create -f TestFiles/4/4.1.nginx-pod.yaml
pod/nginx created
k get po
k get pod nginx --namespace=ckad -o wide
k config get-contexts
k config set-context --current --namespace=ckad
k get po
NAME    READY   STATUS    RESTARTS   AGE
nginx   1/1     Running   0          3m58s
k describe po nginx | grep IP:
k run tmp --image=busybox:1.36.1 -it --rm --restart=Never -- wget -O-  IP
k logs nginx
k run nginx --image=nginx --namespace=ckad --port=80 --env="DB_URL=postgresql://mydb:5432" --env="DB_USERNAME=admin" --dry-run=client -o yaml > TestFiles/4/4.1.nginx-pod-withenv.yaml
k create -f TestFiles/4/4.1.nginx-pod-withenv.yaml 
k exec nginx -- /bin/sh -c "ls -l"

```
</details>

###### 5. Create a YAML manifest for a Pod named loop that runs the busybox:1.36.1 image in a container. The container should run the following command: for i in {1..10}; do echo "Welcome $i times"; done. Create the Pod from the YAML manifest. What’s the status of the Pod? Edit the Pod named loop. Change the command to run in an endless loop. Each iteration should echo the current date. Inspect the events and the status of the Pod loop.
<details>
<summary> Solution</summary>
</details>









###### 

<details>
<summary> Solution</summary>

</details>

