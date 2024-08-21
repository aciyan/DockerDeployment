# DockerDeployment
Setting up a sample project to be deployed in Docker.

## Steps
1. Installed Kubernetes directly -> https://kubernetes.io/docs/tasks/tools/install-kubectl-windows/#install-kubectl-binary-with-curl-on-windows
2. Copy the kubectl.exe file to C:Users\UserName\Kube
3. Added path to environment variable to account
4. Install Docker and enable Kubernetes in Docker.
5. Install Istio -> https://github.com/istio/istio/releases/tag/1.17.1 -> istio-1.17.1-win.zip
6. Extract to C-drive to some folder.
7. Open git bash and set up PATH.
8. Alternatively follow steps metioned in  https://istio.io/latest/docs/setup/install/istioctl/ - https://istio.io/latest/docs/setup/getting-started/#download
9. Execute `istioctl install --set profile=demo -y`
10. Then `kubectl label namespace default istio-injection=enabled`
11. Add docker file to the project (Dockerfile is a text document that contains a set of instructions for building a Docker image). 
12. Specify the entry point as your dll.
13. Build docker image using the command:
 `docker build --tag sampledevsetup`
14. Deploy the docker image in Kubernetes using the below commands, after navigating to the folder containing the yaml files:
```
kubectl apply -f Deployment.yaml
kubectl apply -f Service.yaml
kubectl apply -f Gateway.yaml
kubectl apply -f VirtualService.yaml
```
	1. Deployment.yml file -> Specifies the deployment name, container name and number of replicas needed.
	2. Service.yml -> To access the deployed project, we need to create a service. This is specified by the service file.
	3. Gateway.yml -> In order to access the app deployed in kubernetes from outside, we need to add a gateway (ingress gateway). It specifies the port numbers and protocols used.
    4. VirtualService.yaml - The app is exposed to outside using the virtual service. This file specifies the gateway all requests must be passed to. We can also specify all the protocols, ports and Uris in it.


You can now access the application by logging into http://localhost:80



#### Adding files

```
cd existing_repo
git remote add origin https://gitlab.com/Aciya/dockerdeployment.git
git branch -M main
git push -uf origin main
```
