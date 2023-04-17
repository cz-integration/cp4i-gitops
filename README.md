# cp4i-gitops

This repository mainly demonstrate two approaches to automatically deploy and update IBM MQ instances running on RH OpenShift.

The automation is done with ArgoCD instance installed through Red Hat OpenShift GitOps Operator. 

We'll be using [Kustomize](https://kustomize.io/) to dynamically configure what should be deployed to the cluster. 

This repository holds couple of ArgoCD Applications: 

[Bootstrap](bootstrap.yaml) - Top level application that holds all other applications inside (application of applications)

[operators](operators/) - Application that installs subscription to CP4I related operators

[operands](operands/) - Application that installs instance of Platform Navigator

[namespaces](namespaces/) - Application that creates CP4I namespace 

[qm-alpha](qm-alpha) - Application that installs QM Alpha Queue Manager - approach with commonAnnotation versioning

[myqm](myqm) - Application that installs QM myqm - approach with automatic ConfigMap generator

There are also kustomization.yaml files for some of the applications. This yaml tells what resources should be watched and deployed by ArgoCD. For example, when creating new Queue Manager application, new direcotry with similar structure to qm-alpha and myqm directories. Then this directory would be listed in [kustomization.yaml](kustomization.yaml) to signalize that it should be watched and synced by ArgoCD. 

