## Kubernetes articles and notes


- [Replication Controllers](https://kubernetes.io/docs/concepts/workloads/controllers/replicationcontroller/)

  A __ReplicationController__ ensures that a specified number of pod replicas are running at any one time. In other words, a ReplicationController makes sure that a pod or a homogeneous set of pods is always up and available.
  If there are too many pods, the __ReplicationController__ terminates the extra pods. If there are too few, the ReplicationController starts more pods. _Unlike manually created pods, the pods maintained by a ReplicationController are automatically replaced if they fail, are deleted, or are terminated_. For example, your pods are re-created on a node after disruptive maintenance such as a kernel upgrade. For this reason, you should use a ReplicationController even if your application requires only a single pod. A ReplicationController is similar to a process supervisor, but instead of supervising individual processes on a single node, the ReplicationController supervises multiple pods across multiple nodes.
