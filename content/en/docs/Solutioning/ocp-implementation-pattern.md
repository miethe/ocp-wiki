+++
title = "OpenShift Implementation Patterns"
weight = 5
description = '''
Learn everything Implementation Patterns in OCP.
'''
Date = 2023-04-10
+++

## Implementation Pattern: Migration/Modernization of service to OCP

The services being migrated must have logical separation for the following architectural concerns:

* AuthN/AuthZ
* App Resiliency
* Traffic Management
* External Service Connectivity
* Other Microservice-specific functional concerns

OpenShift Service Mesh is the target solution to meet these architectural concerns. The following patterns will address the above concerns.

### Application Resiliency - Circuit Breaker and Pool Ejection

### AuthN/AuthZ through Service Mesh

### Container Deployments through Service Mesh

Includes the following strategies:

* Canary Deployment
* A/B Deployment
* Traffic Mirroring

## References
