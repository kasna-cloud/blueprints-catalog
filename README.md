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
