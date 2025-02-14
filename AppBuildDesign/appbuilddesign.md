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

###### 5. Create a YAML manifest for a Pod named loop that runs the busybox:1.36.1 image in a container. The container should run the following command: for i in $(seq 4); do echo "Welcome $i times"; done. Create the Pod from the YAML manifest. What’s the status of the Pod? Edit the Pod named loop. Change the command to run in an endless loop. Each iteration should echo the current date. Inspect the events and the status of the Pod loop.
<details>
<summary> Solution</summary>

```
k run loop --image=busybox:1.36.1 --dry-run=client -o yaml -- /bin/sh -c 'for i in $(seq 4); do echo "Welcome $i times"; done' > TestFiles/5/5.loop.yaml
k create -f TestFiles/5/5.loop.yaml
k run loop-endless --image=busybox:1.36.1 --dry-run=client -o yaml -- /bin/sh -c 'while true; do date; sleep 10; done' > TestFiles/5/5.loop-endless.yaml
k create -f TestFiles/5/5.loop-endless.yaml 
k logs loop-endless
```
</details>

###### 6. Create a Job named random-hash using the container image alpine:3.17.3 that executes the shell command echo $RANDOM | base64 | head -c 20. Configure the Job to execute with two Pods in parallel. The number of completions should be set to 5. Identify the Pods that executed the shell command. How many Pods do you expect to exist? Retrieve the generated hash from one of the Pods. Delete the Job. Will the corresponding Pods continue to exist?

<details>
<summary> Solution</summary>

```
k create job random-hash --image=alpine:3.17.3 --dry-run=client -o yaml -- 'bin/sh' -c 'echo $RANDOM | base64 | head -c 20' > TestFiles/6/6.1.randomhash.yaml
k create -f TestFiles/6/6.1.randomhash.yaml
k get po
k logs random-hash-podid
MzAwMDgK
vi add .spec.completions .spec.parallelism


```
</details>

###### 7. Create a new CronJob named google-ping. When executed, the Job should run a curl command for google.com. Pick an appropriate image. The execution should occur every two minutes. Watch the creation of the underlying Jobs managed by the CronJob. Check the command-line options of the relevant command or consult the Kubernetes documentation. Reconfigure the CronJob to retain a history of seven executions. Reconfigure the CronJob to disallow a new execution if the current execution is still running. Consult the Kubernetes documentation for more information.
 

<details>
<summary> Solution</summary>

```
k create cj google-ping --image=nginx:1.26.3 --schedule='*/2 * * * *' --dry-run=client -o yaml -- /bin/sh -c 'curl google.com' >TestFiles/7/7.1.google-ping.yaml
k create -f TestFiles/7/7.1.google-ping.yaml 
k get cj
NAME          SCHEDULE      TIMEZONE   SUSPEND   ACTIVE   LAST SCHEDULE   AGE
google-ping   */2 * * * *   <none>     False     0        21s             3m51s
k get po
NAME                         READY   STATUS      RESTARTS   AGE
google-ping-28992566-wfqr4   0/1     Completed   0          2m36s
google-ping-28992568-tcw9n   0/1     Completed   0          36s

k create cj google-ping --image=nginx:1.26.3 --schedule='*/2 * * * *' --dry-run=client -o yaml -- /bin/sc -c 'curl google.com' >TestFiles/7/7.2.google-ping-history.yaml
vi add .spec.successfulJobsHistoryLimit, .spec.concurrencyPolicy
k create -f Test
k create -f TestFiles/7/7.2.google-ping-history.yaml
k get cj
```
</details>

###### 8. Create a Pod YAML manifest with two containers that use the image alpine:3.12.0. Provide a command for both containers that keep them running forever. Define a Volume of type emptyDir for the Pod. Container 1 should mount the Volume to path /etc/a, and container 2 should mount the Volume to path /etc/b. Open an interactive shell for container 1 and create the directory data in the mount path. Navigate to the directory and create the file hello.txt with the contents “Hello World.” Exit out of the container. Open an interactive shell for container 2 and navigate to the directory /etc/b/data. Inspect the contents of file hello.txt. Exit out of the container.

<details>
<summary> Solution</summary>

```
k run pod --image=alpine:3.12.0 --restart=Always --dry-run=client -o yaml > TestFiles/8/8.1pod.yaml
vi add conatiner 2
add spec.volumes: - name: emptyDIr: {}
add spec.containers.volumeMounts:- name: mountPath: /etc/pod#
k craete -f TestFiles/8/8.1pod.yaml 
k exec -it pod -c pod1 -- /bin/sh
vi add hello.txt file
k exec -it pod -c pod2 -- /bin/sh
cat hello.txt
exit

```
</details>

###### 9. Create a PersistentVolume named logs-pv that maps to the hostPath /var/logs. The access mode should be ReadWriteOnce and ReadOnlyMany. Provision a storage capacity of 5Gi. Ensure that the status of the PersistentVolume shows Available. Create a PersistentVolumeClaim named logs-pvc. It uses ReadWriteOnce access. Request a capacity of 2Gi. Ensure that the status of the PersistentVolume shows Bound. Mount the PersistentVolumeClaim in a Pod running the image nginx at the mount path /var/log/nginx. Open an interactive shell to the container and create a new file named my-nginx.log in /var/log/nginx. Exit out of the Pod. Delete the Pod and re-create it with the same YAML manifest. Open an interactive shell to the Pod, navigate to the directory /var/log/nginx, and find the file you created before.

<details>
<summary> Solution</summary>

```
 vi 9.1.pv.yaml
 apiVersion: v1
 ```
 ```YAML
kind: PersistentVolume
metadata:
 name: logs-pv
spec:
 capacity: 
  storage: 5Gi
 accessModes:
  - ReadWriteOnce
  - ReadOnlyMany
 hostPath:
  path: /var/logs
```
```
k create -f TestFiles/9/9.1.pv.yaml 
k get pv
NAME      CAPACITY   ACCESS MODES   RECLAIM POLICY   STATUS      CLAIM   STORAGECLASS   VOLUMEATTRIBUTESCLASS   REASON   AGE
logs-pv   5Gi        RWO,ROX        Retain           Available                          <unset>                          3s
```
```YAML
apiVersion: v1
kind: PersistentVolumeClaim
metadata: 
 name: logs-pvc
spec: 
 accessModes:
  - ReadWriteOnce
 resources:
  requests:
   storage: 2Gi
```
```
k create -f TestFiles/9/9.2.pvc.yaml 
k run nginx-mount --image=nginx --dry-run=client -o yaml > TestFiles/9/9.3.nginx-mount.yaml
vi nginx-mount.yaml
```
```YAML
spec:
  volumes:
  - name: logs-volume
    persistentVolumeClaim:
      claimName: logs-pvc
```
```YAML
volumeMounts:
    - mountPath: "/var/log/nginx"
      name: logs-volume
```
```
k create -f TestFiles/9/9.3.nginx-mount.yaml 
k exec nginx-mount -it -- /bin/sh
touch //vat/log/my-nginx.log
k delete po nginx-mount
k create -f TestFiles/9/9.3.nginx-mount.yaml 
ls
access.log  error.log  my-nginx.log

k delete po nginx-mount
```

</details>

###### 10. Create a YAML manifest for a Pod named complex-pod. The main application container named app should use the image nginx:1.25.1 and expose the container port 80. Modify the YAML manifest so that the Pod defines an init container named setup that uses the image busybox:1.36.1. The init container runs the command wget -O- google.com. Create the Pod from the YAML manifest. Download the logs of the init container. You should see the output of the wget command. Open an interactive shell to the main application container and run the ls command. Exit out of the container. Force-delete the Pod.

<details>
<summary> Solution</summary>

```

```

</details>

###### 11. Create a YAML manifest for a Pod named data-exchange. The main application container named main-app should use the image busybox:1.36.1. The container runs a command that writes a new file every 30 seconds in an infinite loop in the directory /var/app/data. The filename follows the pattern {counter++}-data.txt. The variable counter is incremented every interval and starts with the value 1. Modify the YAML manifest by adding a sidecar container named sidecar. The sidecar container uses the image busybox:1.36.1 and runs a command that counts the number of files produced by the main-app container every 60 seconds in an infinite loop. The command writes the number of files to standard output. Define a Volume of type emptyDir. Mount the path /var/app/data for both containers. Create the Pod. Tail the logs of the sidecar container. Delete the Pod.

<details>
<summary> Solution</summary>

```
```
</details>


###### 12. Create three Pods that use the image nginx:1.25.1. The names of the Pods should be pod-1, pod-2, and pod-3. Assign the label tier=frontend to pod-1 and the label tier=backend to pod-2 and pod-3. All pods should also assign the label team=artemidis. Assign the annotation with the key deployer to pod-1 and pod-3. Use your own name as the value. From the command line, use label selection to find all Pods with the team artemidis or aircontrol and that are considered a backend service.
<details>
<summary> Solution</summary>

</details>

###### 13. Create a Pod with the image nginx:1.25.1 that assigns two recommended labels: one for defining the application name with the value F5-nginx, and one for defining the tool used to manage the application named helm. Render the assigned labels of the Pod object.

<details>
<summary> Solution</summary>

```
```

</details>


###### 

<details>
<summary> Solution</summary>

</details>

