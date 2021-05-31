# KIX-Blueprints Documentation

This repository contains blueprints to create a GCP Landing Zone.

## Example commands

### List all resources
```
gcloud alpha blueprints list
```

### Apply a blueprint:
```
gcloud alpha blueprints apply
```
Results
```json
{"eventType":"resourceApplied","group":"container.cnrm.cloud.google.com","kind":"ContainerCluster","name":"dan","namespace":"config-controller-system","operation":"Created","timestamp":"2021-05-31T01:08:07Z","type":"apply"}
{"configuredCount":0,"count":1,"createdCount":1,"eventType":"completed","failedCount":0,"serverSideCount":0,"timestamp":"2021-05-31T01:08:07Z","type":"apply","unchangedCount":0}
{"eventType":"completed","pruned":0,"skipped":0,"timestamp":"2021-05-31T01:08:08Z","type":"prune"}
```

### Delete a blueprint:
```
gcloud alpha blueprints delete
```

### Describe a blueprint
```
gcloud alpha blueprints describe
```

### Check the resources you have created:
```
kubectl logs -n cnrm-system -l cnrm.cloud.google.com/component=cnrm-controller-manager -c manager 
```
