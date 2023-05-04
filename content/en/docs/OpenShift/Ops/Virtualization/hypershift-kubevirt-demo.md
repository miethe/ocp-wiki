+++
title = "KubeVirt with HyperShift - Demo"
weight = 10
description = '''
Learn about OpenShift Virtualization
'''
categories = ["Demo", "Lab"]
tags = ["OpenShift", "Virtualization", "KubeVirt", "MetalLB", "HyperShift"]
lab_topics = ["OpenShift", "Virtualization", "MetalLB", "KubeVirt", "HyperShift"]
date = 2023-03-06
+++

## HyperShift and OpenShift Virtualization

------------

The following sections will take you through the steps of:

* Build HyperShift Client
* Configure Environment Variables
* Create HyperShift KubeVirt Hosted Cluster
* Create Ingress Service
* Create Ingress Route
* Examine Hosted Cluster

### Build HyperShift Client

To build the HyperShift client binary. Use the following command to build the CLI tool within a pod:

``` bash
podman run --rm --privileged -it -v \
$PWD:/output docker.io/library/golang:1.18 /bin/bash -c \
'git clone https://github.com/openshift/hypershift.git && \
cd hypershift/ && \
make hypershift && \
mv bin/hypershift /output/hypershift'
```

The binary will be placed under the $PWD directory, move the binary to /usr/local/bin which should be included in the $PATH environment variable:

``` bash
sudo mv $PWD/hypershift /usr/local/bin
```

### Configure Environment Variables

The pull secret is needed for pods accessing images from the registry. Make sure to replace the [PULL\_SECRET](https://console.redhat.com/openshift/install/pull-secret) variable with a path to your pull secret file:

``` bash
export KUBEVIRT_CLUSTER_NAME=kv-00
export PULL_SECRET="/path/to/pull-secret"
```

### Create HyperShift KubeVirt Hosted Cluster

Use the following command to create a node pool of 2 workers and the guest cluster [playload](https://mirror.openshift.com/pub/openshift-v4/x86_64/clients/ocp/4.12.3/release.txt) [version](https://mirror.openshift.com/pub/openshift-v4/x86_64/clients/ocp/4.12.3/release.txt) can be specified by \`--release-image\`. Starting from 4.12.2, a default ingress passthrough feature is added, we no longer need to create ingress services and routes manually.

``` bash
hypershift create cluster \
kubevirt \
--name $KUBEVIRT_CLUSTER_NAME \
--node-pool-replicas=2 \
--memory '8Gi' \
--pull-secret $PULL_SECRET \
--release-image=quay.io/openshift-release-dev/ocp-release@sha256:382f271581b9b907484d552bd145e9a5678e9366330059d31b007f4445d99e36
```

It takes some time for the VMs to be provisioned, you can use the following command to wait until the VM workers reach ready state:

``` bash
oc wait --for=condition=Ready --namespace $KUBEVIRT_CLUSTER_NAMESPACE vm --all --timeout=600s
```

Once the VM workers are ready, we can generate the guest cluster kubeconfig file which is useful when we want to examine the guest cluster.

``` bash
hypershift create kubeconfig --name="$KUBEVIRT_CLUSTER_NAME" > "${KUBEVIRT_CLUSTER_NAME}-kubeconfig"
```

### Examine The Hosted Cluster

Once all the guest cluster operators are deployed successfully, the status of the Available column should be True and the PROGRESS column should be changed to Completed. We created three guest clusters with different releases just to show that it is possible to manage multi-version hosted clusters in HyperShift with the KubeVirt provider:

``` bash
[root@e24-h21-740xd hypershift]# oc get hc -A
NAMESPACE   NAME    VERSION   KUBECONFIG               PROGRESS    AVAILABLE   PROGRESSING   MESSAGE
clusters    kv-00   4.12.2    kv-00-admin-kubeconfig   Completed   True        False         The hosted control plane is available
clusters    kv-04   4.12.3    kv-04-admin-kubeconfig   Completed   True        False         The hosted control plane is available
clusters    kv-05   4.12.4    kv-05-admin-kubeconfig   Completed   True        False         The hosted control plane is available
```

If we take a closer look, there is a dedicated namespace \`clusters-kv-00\` being created for the hosted control plane. Under this namespace, we should be able see control plane pods such as etcd and  kube-api-server are running:

``` bash
[root@e24-h21-740xd ~]# oc get pod -n clusters-kv-00 | grep 'kube-api\|etcd'
etcd-0                                                2/2     Running     0          47h
kube-apiserver-864764b74b-t2tcl                       3/3     Running     0          47h
```

There are two virt-launcher pods for the KubeVirt virtual machines since we specified \`node-pool-replicas=2\`:

``` bash
[root@e24-h21-740xd ~]# oc get pod -n clusters-kv-00 | grep 'virt-launcher'
virt-launcher-kv-00-j45fr-mt5lc                       1/1     Running     0          2d1h
virt-launcher-kv-00-l7f27-fk9tj                       1/1     Running     0          2d1h
```

To check the status of those two VMs:

``` bash
[root@e24-h21-740xd ~]# oc get vm -n clusters-kv-00
NAME          AGE    STATUS    READY
kv-00-j45fr   2d1h   Running   True
kv-00-l7f27   2d1h   Running   True
```

To examine our guest clusters, we need to have the oc tool pointing to the guest kubeconfig. From OCP’s perspective, these two virtual machines will be the worker nodes:

``` bash
[root@e24-h21-740xd hypershift]# oc --kubeconfig kv-00-kubeconfig get nodes
NAME          STATUS   ROLES    AGE    VERSION
kv-00-j45fr   Ready    worker   2d1h   v1.25.4+77bec7a
kv-00-l7f27   Ready    worker   2d1h   v1.25.4+77bec7a
```

We should also be able to see that there is a dedicated monitoring and networking stack for each guest cluster:

``` bash
[root@e24-h21-740xd hypershift]# oc --kubeconfig kv-00-kubeconfig get pod -A | grep 'prometh\|ovn\|ingress'
openshift-ingress-canary                           ingress-canary-j4lq4                                     1/1     Running     0              2d1h
openshift-ingress-canary                           ingress-canary-zd28w                                     1/1     Running     0              2d1h
openshift-ingress                                  router-default-68df75f88d-dszb2                          1/1     Running     0              2d1h
openshift-monitoring                               prometheus-adapter-6fd546d669-c2dw6                      1/1     Running     0              2d1h
openshift-monitoring                               prometheus-k8s-0                                         6/6     Running     0              2d1h
openshift-monitoring                               prometheus-operator-688459b4f4-45775                     2/2     Running     0              2d1h
openshift-monitoring                               prometheus-operator-admission-webhook-849b6cd6bf-52rpq   1/1     Running     0              2d1h
openshift-ovn-kubernetes                           ovnkube-node-4hmgz                                       5/5     Running     4 (2d1h ago)   2d1h
openshift-ovn-kubernetes                           ovnkube-node-87nk7                                       5/5     Running     0              2d1h
```

## Summary

------------

We went through the detailed steps of installing and configuring necessary operators and controllers to set up HyperShift with the KubeVirt provider in an existing bare metal OCP cluster environment. We also demonstrated how to launch a hosted cluster using the HyperShift command line tool, examined where the hosted control planes pods are running and what components are being placed inside of guest clusters.
