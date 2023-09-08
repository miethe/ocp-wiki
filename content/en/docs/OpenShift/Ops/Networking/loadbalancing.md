+++
title = "Networking"
description = '''
Load Balancing and external service access in OpenShift.
'''
categories = ["Engineering"]
tags = ["OpenShift", "Networking", "Ingress", "Load Balancer", "External IP"]
+++

Whenever a service needs to be accessed from outside a cluster (external to the network), there are several options available. The primary and most appropriate method is through using a Load Balancer. However, in some situations, such as during dev or test in an ephemeral or local cluster, it is easier to use methods such as exposing NodePorts. In this post, we will be explaining the various options available.

## Load Balancers

### HAproxy - OCP Default

### MetalLB

MetalLB is a powerful Load Balancer available as an Operator in OpenShift which provides Load Balancing for clusters deployed on bare-metal or other environments without native load balancers: on-prem, IBM Power, Z, vSphere, etc.

MetalLB can operate on either L2 or L3, in addition to utilizing BGP. While the L2 functionality is similar to IP failover, it leverages a gossip-based protocol to identify node failure, via **VRRP** and `keepalived`. This makes MetalLB preferable over more basic options like IP failover.

The MetalLB Operator works within the cluster by providing a platform-native load balancer to any `Service` of type `LoadBalancer`, automating the entire process for every `Service`.

## Other Methods

### NodePorts

One of the most simple methods for exposing a `Service` outside of a cluster is by using a `NodePort`. `Nodeports` are a specific port on all OpenShift hosts (nodes) which is assigned to a specific service. This allows access to the service in a similar manner to accessing the OpenShift Web Console, at the core OpenShift IP but at the given port.

Assuming you have a `Service` which you are trying to expose, you can do the following to create a `NodePort`:

From within the given `project`:

```bash
oc edit svc <service_name>
```

```yaml
spec:
  ports:
  - name: 8443-tcp
    nodePort: 31234
    port: 8443
    protocol: TCP
    targetPort: 8443
  sessionAffinity: None
  type: NodePort
```

Validate your service is updated w/ the given port:

```bash
oc get svc
```

```bash
NAME    TYPE       CLUSTER-IP      EXTERNAL-IP   PORT(S)          AGE
httpd   NodePort   172.xx.xx.xx    <none>        8443:31234/TCP   12s
```

## Resources

* [Using Integrated Load Balancing With On-Premises OpenShift 4 IPI](https://cloud.redhat.com/blog/using-integrated-load-balancing-with-on-premises-openshift-4-ipi)
* [Configuring ingress cluster traffic using a NodePort - Configuring ingress cluster traffic | Networking | OpenShift Container Platform 4.13](https://docs.openshift.com/container-platform/4.13/networking/configuring_ingress_cluster_traffic/configuring-ingress-cluster-traffic-nodeport.html)
* [About MetalLB and the MetalLB Operator - Load balancing with MetalLB | Networking | OpenShift Container Platform 4.13](https://docs.openshift.com/container-platform/4.13/networking/metallb/about-metallb.html)