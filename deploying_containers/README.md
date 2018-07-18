This section will cover how to go about the orchestration, configuration and deployment of containers. 

Technologies I'm most interested in to accomplish this are Terraform, Ansible, Airflow, and obviously, Kubernetes and Docker.

I will look at each of them in a stand-alone sense as well as in a cohesive product. Self healing solutions will also have a heavy focus.




# Kubernetes


Kubernetes
- Master -- can this be my localhost? Should it?
- Nodes -- a Kubernetes instance that handles production traffic should have >= 3 nodes.


You can create and manage a Deployment by using the Kubernetes command line interface, __Kubectl__. 

The common format of a kubectl command is: `kubectl` `action` `resource`. 

Let’s run our first app on Kubernetes with the `kubectl run` command. The run command creates a new deployment. We need to provide the deployment name and app image location (include the full repository url for images hosted outside Docker hub). We want to run the app on a specific port so we add the `--port` parameter:

```bash
kubectl run kubernetes-bootcamp --image=gcr.io/google-samples/kubernetes-bootcamp:v1 --port=8080
```

To list your deployments use the get deployments command:

`kubectl get deployments`

```
$ curl http://localhost:8001/version
{
  "major": "1",
  "minor": "10",
  "gitVersion": "v1.10.0",
  "gitCommit": "fc32d2f3698e36b93322a3465f63a14e9f0eaead",
  "gitTreeState": "clean",
  "buildDate": "2018-04-10T12:46:31Z",
  "goVersion": "go1.9.4",
  "compiler": "gc",
  "platform": "linux/amd64"
}$ export POD_NAME=$(kubectl get pods -o go-template --template '{{range .items}}{{.metadata.name}}{{"\n"}}{{end}}')
$ echo Name of the Pod: $POD_NAME
Name of the Pod: kubernetes-bootcamp-5c69669756-sxvjd
$ curl http://localhost:8001/api/v1/namespaces/default/pods/$POD_NAME/proxy/
Hello Kubernetes bootcamp! | Running on: kubernetes-bootcamp-5c69669756-sxvjd | v=1
```


A Pod models an application-specific "logical host" and can contain different application containers which are relatively tightly coupled. For example, a Pod might include both the container with your Node.js app as well as a different container that feeds the data to be published by the Node.js webserver. The containers in a Pod share an IP Address and port space, are always co-located and co-scheduled, and run in a shared context on the same Node.

### Pods Overview
![Pods Overview](https://d33wubrfki0l68.cloudfront.net/fe03f68d8ede9815184852ca2a4fd30325e5d15a/98064/docs/tutorials/kubernetes-basics/public/images/module_03_pods.svg)

Note: 
* Pod1 = 1 container
* Pod4 = 3 containers (3 different applications) with 2 volumes -- all have shared IP address

