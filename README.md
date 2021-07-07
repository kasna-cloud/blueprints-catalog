# Overview

This repository contains the building blocks that can be used to create a landing zone only after Config Sync has been created. See [blueprints-landing-zone](https://gitlab.mantelgroup.com.au/kasna/kix/blueprints-landing-zone).

# KIX-Blueprints Documentation

This repository contains blueprints to create a GCP Landing Zone.

# Example commands

## Apply a blueprint:
```
gcloud alpha blueprints apply
```
#### Output
```json
{"eventType":"resourceApplied","group":"container.cnrm.cloud.google.com","kind":"ContainerCluster","name":"dan","namespace":"config-controller-system","operation":"Created","timestamp":"2021-05-31T01:08:07Z","type":"apply"}
{"configuredCount":0,"count":1,"createdCount":1,"eventType":"completed","failedCount":0,"serverSideCount":0,"timestamp":"2021-05-31T01:08:07Z","type":"apply","unchangedCount":0}
{"eventType":"completed","pruned":0,"skipped":0,"timestamp":"2021-05-31T01:08:08Z","type":"prune"}
```
## Delete a blueprint:
```
gcloud alpha blueprints delete
```
#### Output:
```json
{"eventType":"resourceDeleted","group":"container.cnrm.cloud.google.com","kind":"ContainerCluster","name":"dan","namespace":"config-controller-system","operation":"Deleted","timestamp":"2021-05-31T01:11:24Z","type":"delete"}
{"deleted":1,"eventType":"completed","skipped":0,"timestamp":"2021-05-31T01:11:27Z","type":"delete"}
```
## List all resources
```
gcloud alpha blueprints list
```
## Describe a blueprint
```
gcloud alpha blueprints describe
```
## Check the resources you have created:
```
kubectl logs -n cnrm-system -l cnrm.cloud.google.com/component=cnrm-controller-manager -c manager 
```

# Important
Blueprints require a GKE cluster to operate. To save on costs, the cluster will be terminated each night. To start up a cluster follow the documentation [here](https://mantelgroup.atlassian.net/wiki/spaces/~440540889/pages/4039409672/Useful+Commands).
