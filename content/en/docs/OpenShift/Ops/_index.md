+++
title = "OCP Ops"
weight = 1
description = '''
Ops topics within OpenShift
'''
categories = ["Engineering"]
tags = ["OpenShift"]
+++

## OpenShift vs Kubernetes

A common misconception is that OpenShift is a different type of container orchestration tool, or that it is Kubernetes, but completely locked-down and different.

The truth is, OpenShift **is** Kubernetes! Red Hat was one of the first industry supporters of Kubernetes prior to it's open-source release, and OpenShift was the first vendor-distribution. Due to being so early, the OpenShift development team created a number of components which eventually made it upstream into Kubernetes (like RBAC), as well as varying solutions to problems that eventually reached different resolutions in Kubernetes (Routes vs Ingress). However, even for the latter, OpenShift still fully supports upstream Kubernetes features, while at times adding a wrapper or additional functionality on top.

In this section, we review many of the unique features in OpenShift as well as OCP-specific implementations of common resources.
