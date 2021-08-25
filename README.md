# Overview

This repository contains the building blocks that can be used to create a landing zone only after Config Sync has been created. See [blueprints-landing-zone](https://gitlab.mantelgroup.com.au/kasna/kix/blueprints-landing-zone).

# Prerequisites

This section goes through step by step process to start with Google Cloud.

# Setting up the device

[Go to Google cloud](https://cloud.google.com)
Sign up if you don’t have google account and go to console.

## Open terminal

* To go to your root directory type 
```sh
cd ~/
```
* To make the directory type 
```bash
mkdir ${UNIQUE_DIRECTORY_NAME}
```
```bash
cd ${UNIQUE_DIRECTORY_NAME}
```
* To install the Google Cloud SDK, type
```
curl https://sdk.cloud.google.com | bash
```
* Open new terminal

```
gcloud auth login
```
* Follow the prompts
* You will see a prompt to set project id
```bash
gcloud config set project ${YOUR_PROJECT_NAME}
```
* To install kpt
```
gcloud components install kpt
```

# Example commands

## Apply a blueprint:
```
gcloud alpha blueprints apply --source=./<corresponding-blueprint-folder> <RESOURCE-NAME>
```
* Resource name used in this command should be the same as the one used in metadata in setters.yaml

#### Output
```json
{"eventType":"resourceApplied","group":"container.cnrm.cloud.google.com","kind":"ContainerCluster","name":"dan","namespace":"config-controller-system","operation":"Created","timestamp":"2021-05-31T01:08:07Z","type":"apply"}
{"configuredCount":0,"count":1,"createdCount":1,"eventType":"completed","failedCount":0,"serverSideCount":0,"timestamp":"2021-05-31T01:08:07Z","type":"apply","unchangedCount":0}
{"eventType":"completed","pruned":0,"skipped":0,"timestamp":"2021-05-31T01:08:08Z","type":"prune"}
```
## Delete a blueprint:
```
gcloud alpha blueprints delete <RESOURCE-NAME>
```

* Resource name used in this command should be the same as the one used in metadata in setters.yaml

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
## Tested
- Big Table
- BigQuery
- Cloud SQL
