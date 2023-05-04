+++
title = "Operators"
weight = 4
description = '''
Learn more about Operators.
'''
categories = ["Engineering"]
tags = ["OpenShift", "Operators", "K8s", "Go", "Ansible", "Helm"]
+++

## What is it

Operators automate the creation, configuration, and management of instances of Kubernetes-native applications. Operators provide automation at every level of the stack—from managing the parts that make up the platform all the way to applications that are provided as a managed service.

### Operators with OpenShift

{{< img src="operator-phases.png" width="1100" >}}

Red Hat OpenShift uses the power of Operators to run the entire platform in an autonomous fashion while exposing configuration natively through Kubernetes objects, allowing for quick installation and frequent, robust updates. In addition to the automation advantages of Operators for managing the platform, Red Hat OpenShift makes it easier to find, install, and manage Operators running on your clusters.

OpenShift uses Operators extensively for the management of the container platform, internal services, and many workloads.

[What are OCP Operators?](https://www.redhat.com/en/technologies/cloud-computing/openshift/what-are-openshift-operators)

### Helm

### Ansible

### Go

## Why/When use it

## How to use it

### Operator SDK

There are multiple paths to create your own Operator. One of the easiest routes, and typically most preferred for usage on OpenShift, is the [Operator SDK](https://github.com/operator-framework/operator-sdk){{< icons/github >}}.

Operator SDK is a component of the [Operator Framework](https://sdk.operatorframework.io/).

## Examples

* [Example Operators](https://github.com/operator-framework/operator-sdk/tree/master/testdata) - The Operator SDK offers an example for each type of Operator.

## References

### More Information

* [What is a Kubernetes operator?](https://www.redhat.com/en/topics/containers/what-is-a-kubernetes-operator)
* [Demystifying Operator Development](https://www.ibm.com/cloud/blog/demystifying-operator-development)

### Operator SDK Guides/Demos

* [James-Hope/operator-sdk-demo: Skeleton Ansible based operator built using SDK-Operator library](https://github.ibm.com/James-Hope/operator-sdk-demo) {{< icons/github >}}
* [Certified Operator Build Guide](https://redhat-connect.gitbook.io/certified-operator-guide/) - Outlines Helm, Ansible, and Go Operator builds, as well as the OCP Deployment and Certification Process.
* [Partner Guide for OpenShift and Container Certification](https://redhat-connect.gitbook.io/partner-guide-for-red-hat-openshift-and-container/)
* [atarazana/gramola-operator](https://github.com/atarazana/gramola-operator){{< icons/github >}} - old, but good lab and demo around Operators, answering Why and How.

### Operator Courses

These courses include learning about all forms of Operators, such as Go, Helm, Ansible, and Operator SDK.

* [Kubernetes Operators Intermediate](https://cognitiveclass.ai/courses/kubernetes-operators-intermediate)
* [Kubernetes Operators Advanced](https://cognitiveclass.ai/courses/course-v1:IBM+CO0302EN+v1)