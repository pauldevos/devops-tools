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

Some definitions:
A Pod always runs on a **Node**. A Node is a `worker machine` in Kubernetes and may be either a _virtual_ or a _physical machine_, depending on the cluster.

Each `Node` is managed by the `Master`. A Node can have multiple pods, and the Kubernetes master automatically handles scheduling the pods across the Nodes in the cluster. The Master's automatic scheduling takes into account the available resources on each Node.

```
$ kubectl get pods
NAME                                   READY     STATUS    RESTARTS   AGE
kubernetes-bootcamp-5c69669756-8dn6j   1/1       Running   0          11s
$ kubectl describe pods
Name:           kubernetes-bootcamp-5c69669756-8dn6j
Namespace:      default
Node:           minikube/172.17.0.12
Start Time:     Wed, 18 Jul 2018 21:04:54 +0000
Labels:         pod-template-hash=1725225312
                run=kubernetes-bootcamp
Annotations:    <none>
Status:         Running
IP:             172.18.0.2
Controlled By:  ReplicaSet/kubernetes-bootcamp-5c69669756
Containers:
  kubernetes-bootcamp:
    Container ID:   docker://97c4454f55086677a96ebe3a1b4881691121d14ed135b637fd6a9dd969b5284f
    Image:          gcr.io/google-samples/kubernetes-bootcamp:v1
    Image ID:       docker-pullable://gcr.io/google-samples/kubernetes-bootcamp@sha256:0d6b8ee63bb57c5f5b6156f446b3bc3b3c143d233037f3a2f00e279c8fcc64af
    Port:           8080/TCP
    Host Port:      0/TCP
    State:          Running
      Started:      Wed, 18 Jul 2018 21:04:55 +0000
    Ready:          True
    Restart Count:  0
    Environment:    <none>
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from default-token-mw7zd (ro)
Conditions:
  Type           Status
  Initialized    True
  Ready          True
  PodScheduled   True
Volumes:
  default-token-mw7zd:
    Type:        Secret (a volume populated by a Secret)
    SecretName:  default-token-mw7zd
    Optional:    false
QoS Class:       BestEffort
Node-Selectors:  <none>
Tolerations:     node.kubernetes.io/not-ready:NoExecute for 300s
                 node.kubernetes.io/unreachable:NoExecute for 300s
Events:
  Type     Reason                 Age                From               Message
  ----     ------                 ----               ----               -------
  Warning  FailedScheduling       17s (x4 over 20s)  default-scheduler  0/1 nodes are available: 1 node(s) were not ready.
  Normal   Scheduled              13s                default-scheduler  Successfully assigned kubernetes-bootcamp-5c69669756-8dn6j to minikube
  Normal   SuccessfulMountVolume  13s                kubelet, minikube  MountVolume.SetUp succeeded for volume "default-token-mw7zd"
  Normal   Pulled                 12s                kubelet, minikube  Container image "gcr.io/google-samples/kubernetes-bootcamp:v1" already present on machine
  Normal   Created                12s                kubelet, minikube  Created container
  Normal   Started                12s                kubelet, minikube  Started container
```

Recall that Pods are running in an isolated, private network - so we need to proxy access to them so we can debug and interact with them. To do this, we'll use the kubectl proxy command to run a proxy in a second terminal window. Click on the command below to automatically open a new terminal and run the proxy:

`kubectl proxy`

Now again, we'll get the Pod name and query that pod directly through the proxy. To get the Pod name and store it in the POD_NAME environment variable:

`export POD_NAME=$(kubectl get pods -o go-template --template '{{range .items}}{{.metadata.name}}{{"\n"}}{{end}}')
echo Name of the Pod: $POD_NAME`

To see the output of our application, run a curl request.

`curl http://localhost:8001/api/v1/namespaces/default/pods/$POD_NAME/proxy/`

The url is the route to the API of the Pod.

Anything that the application would normally send to `STDOUT` becomes logs for the container within the Pod. We can retrieve these logs using the `kubectl logs` command:

`kubectl logs $POD_NAME`


```
$ kubectl describe pods
Name:           kubernetes-bootcamp-5c69669756-8dn6j
Namespace:      default
Node:           minikube/172.17.0.12
Start Time:     Wed, 18 Jul 2018 21:04:54 +0000
Labels:         pod-template-hash=1725225312
                run=kubernetes-bootcamp
Annotations:    <none>
Status:         Running
IP:             172.18.0.2
Controlled By:  ReplicaSet/kubernetes-bootcamp-5c69669756
Containers:
  kubernetes-bootcamp:
    Container ID:   docker://97c4454f55086677a96ebe3a1b4881691121d14ed135b637fd6a9dd969b5284f
    Image:          gcr.io/google-samples/kubernetes-bootcamp:v1
    Image ID:       docker-pullable://gcr.io/google-samples/kubernetes-bootcamp@sha256:0d6b8ee63bb57c5f5b6156f446b3bc3b3c143d233037f3a2f00e279c8fcc64af
    Port:           8080/TCP
    Host Port:      0/TCP
    State:          Running
      Started:      Wed, 18 Jul 2018 21:04:55 +0000
    Ready:          True
    Restart Count:  0
    Environment:    <none>
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from default-token-mw7zd (ro)
Conditions:
  Type           Status
  Initialized    True
  Ready          True
  PodScheduled   True
Volumes:
  default-token-mw7zd:
    Type:        Secret (a volume populated by a Secret)
    SecretName:  default-token-mw7zd
    Optional:    false
QoS Class:       BestEffort
Node-Selectors:  <none>
Tolerations:     node.kubernetes.io/not-ready:NoExecute for 300s
                 node.kubernetes.io/unreachable:NoExecute for 300s
Events:
  Type     Reason                 Age              From               Message
  ----     ------                 ----             ----               -------
  Warning  FailedScheduling       3m (x4 over 3m)  default-scheduler  0/1 nodes are available: 1 node(s) were not ready.
  Normal   Scheduled              3m               default-scheduler  Successfully assigned kubernetes-bootcamp-5c69669756-8dn6j to minikube
  Normal   SuccessfulMountVolume  3m               kubelet, minikube  MountVolume.SetUp succeeded for volume "default-token-mw7zd"
  Normal   Pulled                 3m               kubelet, minikube  Container image "gcr.io/google-samples/kubernetes-bootcamp:v1" already present on machine
  Normal   Created                3m               kubelet, minikube  Created container
  Normal   Started                3m               kubelet, minikube  Started container
$ export POD_NAME=$(kubectl get pods -o go-template --template '{{range .items}}{{.metadata.name}}{{"\n"}}{{end}}')
$ echo Name of the Pod: $POD_NAME
Name of the Pod: kubernetes-bootcamp-5c69669756-8dn6j
$ curl http://localhost:8001/api/v1/namespaces/default/pods/$POD_NAME/proxy/
Hello Kubernetes bootcamp! | Running on: kubernetes-bootcamp-5c69669756-8dn6j | v=1
$ kubectl logs $POD_NAME
Kubernetes Bootcamp App Started At: 2018-07-18T21:04:55.341Z | Running On:  kubernetes-bootcamp-5c69669756-8dn6j

Running On: kubernetes-bootcamp-5c69669756-8dn6j | Total Requests: 1 | App Uptime: 226.123 seconds | Log Time: 2018-07-18T21:08:41.464Z
$ kubectl exec $POD_NAME env
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
HOSTNAME=kubernetes-bootcamp-5c69669756-8dn6j
KUBERNETES_PORT=tcp://10.96.0.1:443
KUBERNETES_PORT_443_TCP=tcp://10.96.0.1:443
KUBERNETES_PORT_443_TCP_PROTO=tcp
KUBERNETES_PORT_443_TCP_PORT=443
KUBERNETES_PORT_443_TCP_ADDR=10.96.0.1
KUBERNETES_SERVICE_HOST=10.96.0.1
KUBERNETES_SERVICE_PORT=443
KUBERNETES_SERVICE_PORT_HTTPS=443
NPM_CONFIG_LOGLEVEL=info
NODE_VERSION=6.3.1
HOME=/root
$ kubectl exec -ti $POD_NAME bash
root@kubernetes-bootcamp-5c69669756-8dn6j:/# ls
bin  boot  core  dev  etc  home  lib  lib64  media  mnt  opt  proc  root  run  sbin  server.js  srv  sys  tmp  usr  var
root@kubernetes-bootcamp-5c69669756-8dn6j:/# cat server.js
var http = require('http');
var requests=0;
var podname= process.env.HOSTNAME;
var startTime;
var host;
var handleRequest = function(request, response) {
  response.setHeader('Content-Type', 'text/plain');
  response.writeHead(200);
  response.write("Hello Kubernetes bootcamp! | Running on: ");
  response.write(host);
  response.end(" | v=1\n");
  console.log("Running On:" ,host, "| Total Requests:", ++requests,"| App Uptime:", (new Date() - startTime)/1000 , "seconds", "| Log Time:",new Date());
}
var www = http.createServer(handleRequest);
www.listen(8080,function () {
    startTime = new Date();;
    host = process.env.HOSTNAME;
    console.log ("Kubernetes Bootcamp App Started At:",startTime, "| Running On: " ,host, "\n" );
});
root@kubernetes-bootcamp-5c69669756-8dn6j:/# curl localhost:8080
Hello Kubernetes bootcamp! | Running on: kubernetes-bootcamp-5c69669756-8dn6j | v=1
root@kubernetes-bootcamp-5c69669756-8dn6j:/# exit
exit
```
