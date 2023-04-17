# Deploying Queue Manager with dynamic ConfigMap generation

This application demonstrates how to trigger Queue Manager redeployment (Rolling Update) when ConfigMaps with MQSC gets updated. 

See [kustomization.yaml](resources/kustomization.yaml) for details. Starting on line 8, by `configMapGenerator` line, this file specifies that a ConfigMap should be automatically generated from a `myqm.mqsc` file. The ConfigMap is generated when change in the `myqm.mqsc` file is detected and it's synchronized by ArgoCD application - it is generated under the specified name (`myqm-config`) and a random ID is added to the end of the name. The [kustomization-config-mq.yaml](resources/kustomization-config-mq.yaml) file then specifies, that the name of this newly generated ConfigMap should be added to the QueueManger specification which is referenced at the end of the [kustomization.yaml](resources/kustomization.yaml) file. This change in the name of the ConfigMap in the MQ YAML triggers the Rolling Update of the MQ instance. 

More resources could be generated like this - ConfigMap with a qm.ini file, Secrets with PKI information etc. 