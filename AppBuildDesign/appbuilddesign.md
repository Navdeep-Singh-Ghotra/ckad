## Application Design and Build
- Define, build and modify container images
- Choose and use the right workload resource (Deployment, DaemonSet, CronJob, etc.)
- Understand multi-container Pod design patterns (e.g. sidecar, init and others)
- Utilize persistent and ephemeral volumes

### Define, build and modify container images
<details>

<summary>Navigate to the directory app-a/ch04/containerized-java-app of the checked-out GitHub repository bmuschko/ckad-study-guide. Inspect the Dockerfile.

Build the container image from the Dockerfile with the tag nodejs-hello-world:1.0.0.

Run a container with the container image. Make the application available on port 80.

Execute a curl or wget command against the application’s endpoint.

Retrieve the container logs.</summary>

### Answer :

run the command: 
```k run nginx --image=nginx --dry-run=client -o yaml > 1.yaml```


</details>

