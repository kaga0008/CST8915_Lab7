# CST8915 Lab 7
## Elizabeth Kaganovsky (040956095)

### Video link: 


### RabbitMQ Issues
RabbitMQ is a stateful application, meaning that it retains information and therefore requires persistent storage to function properly. This clashes with the main principle behind containers, which is their ephemerality. When RabbitMQ runs in a container without persistent storage, every restart of the container container causes the entire contents of the file system to be lost.

As for potential solutions, the remedy lies in persistent volumes (PVs):

First, a PV must be created, which can be done in the .YAML file. A PV is provisioned at the cluster level, and can be shared between multiple namespaces. Then, a persistent volume claim (PVC) must be provisioned, to allow the application to "claim" some of the persistent storage allocated to the cluster. That PVC can then be used in the pod configuration (under "spec" would be "volumes" with the PV and PVC). The volume is then mounted to the pod, allowing the pod (and all containers within) access to it for persistent storage.

Alternatively, Azure Service Bus can be used in place of RabbitMQ, since it provides a fully-managed message broker that supports message queues and leaves the storage and scaling to Azure rather than the application operator.