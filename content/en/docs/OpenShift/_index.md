+++
title = "OpenShift"
weight = 5
description = '''
Learn more about OpenShift
'''
categories = ["Engineering"]
tags = ["OpenShift"]
+++

## What is it

### OpenShift

**OpenShift** is simply, at its core, Red Hat’s opinion on Kubernetes. OpenShift is based on the latest upstream Kubernetes version, with various enhancements on top. Usually, these enhancements eventually make their way into later k8s versions.In fact, many of the core Kubernetes features were forked from, or inspired by, OpenShift functionality; ie, Ingress.

OpenShift was first released in 2011 as a proprietary Linux container-based PaaS, but was quickly became open-source. OpenShift v3 was eventually released as a major refactor based upon Kubernetes, which had recently been released. OpenShift was moved to its current, and most powerful, form with v4, shifting to CRI-O, Podman, and Buildah, along with other major architectural changes. OpenShift is currently on {{< param "ocp_version" >}}.

### OCP

However, there’s more to OpenShift than a few new features, which leads into **OpenShift Container Platform** (OCP). OCP is more than a simple flavor of Kubernetes; it is an entire ecosystem for the development and deployment of applications. With traditional k8s deployments, each individual component must be chosen, integrated, and maintained in order to create a proper and fully-featured devops infrastructure. OCP, however, provides such native integrations out-of-the-box from Day 1, with included offerings such as OpenShift Pipelines (based on Tekton & ArgoCD), Logging, Security (Stackrox), Service Mesh (Istio-based), and many others.

One primary advantage with these integrations that differentiates OCP from other similar services, is where every single component is configurable, optional, and modifiable. That means you can use as much, or as little, of the RH-offered integrations as you like, and bring your own when desired.

## Examples

## References

### Links to Learn More

### Links to Education Content

* [OCP on IBM Cloud](https://developer.ibm.com/openlabs/openshift)
* [RH Learn](https://learn.openshift.com/)

### General OpenShift Courses

* [Hands-on with Red Hat OpenShift: Deploy, Scale & Manage Apps](https://cognitiveclass.ai/courses/hands-on-with-red-hat-openshift-app-lifecycle)

### Try it
