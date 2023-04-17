# Deploying Queue Manager with commonAnnotations approach

This application demonstrates how to trigger Queue Manager redeployment (Rolling Update) when ConfigMaps with MQSC gets updated. 

See [kustomization.yaml](resources/kustomization.yaml) for details. Starting on line 7, by `commonAnnotations` line, this file specifies that all objects listed under `resources` on line 4 should be annotated with `qm-alpha/version` tag. 
When changing the ConfigMap with MQSC script in it, in order to propagate this change to a Queue Manager, this value needs to be updated to a new version number. When ArgoCD synchronizes this Annotation change on the existing MQ instance, it automatically triggers a RollingUpdate. 

More resources could be added and annotated with this approach - ConfigMaps with qm.ini files, Secrets with PKI information etc. 