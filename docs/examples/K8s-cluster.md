# K8s Cluster

The [k8s-cluster](../../examples/k8s-cluster.pentestrc) pentestrc resource file define a basic, insecure Kubernetes cluster, composed of one master and two nodes:
```
> PENTESTRC=examples/k8s-cluster.pentestrc vagrant status
Current machine states:

k8s-master                not created (virtualbox)
k8s-node1                 not created (virtualbox)
k8s-node2                 not created (virtualbox)

This environment represents multiple VMs. The VMs are all listed
above with their current state. For more information about a specific
VM, run `vagrant status NAME`.
```

Spawn the cluster with `vagrant up` command:
```
> export PENTESTRC=examples/k8s-cluster.pentestrc 
> vagrant up
```

Once provisioned, pods should be running:
```
> vagrant ssh k8s-master -- kubectl get pods  
NAME                          READY     STATUS    RESTARTS   AGE
dvwa-3174703020-6mmmt         1/1       Running   1          13m
phpmailer-81832430-dnbbn      1/1       Running   0          13m
shellshock-2092454790-m95fj   1/1       Running   0          13m
```
