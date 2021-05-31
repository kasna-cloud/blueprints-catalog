# KIX-Blueprints Documentation

This repository contains blueprints to create a GCP Landing Zone.

## Get Started

```
gcloud components install kpt alpha
```

```
gcloud services enable config.googleapis.com
```

```
export PROJECT_ID=$(gcloud config get-value project)
```

```
export PROJECT_NUM=$(gcloud projects list --filter="${PROJECT_ID}" --format="value(PROJECT_NUMBER)" | tail -1)
```

```
gcloud compute networks create default --subnet-mode=auto
```

```
gcloud beta services identity create --service=krmapihosting.googleapis.com
```

```
gcloud beta services identity create --service=config.googleapis.com
```

```
export CNRM_SA="service-$PROJECT_NUM@gcp-sa-yakima.iam.gserviceaccount.com"
```

```
gcloud projects add-iam-policy-binding ${PROJECT_ID}
--member=serviceAccount:${PROJECT_NUM}@cloudbuild.gserviceaccount.com
--role=roles/container.developer
```

```
gcloud projects add-iam-policy-binding ${PROJECT_ID} --member=serviceAccount:${PROJECT_NUM}@cloudbuild.gserviceaccount.com --role=roles/container.clusterViewer
```

```
gcloud projects add-iam-policy-binding ${PROJECT_ID} --role=roles/owner --condition=None --member="serviceAccount:${CNRM_SA}"
```

### Create a Blueprints GKE Cluster creates a GKE cluster named krmapihost-blueprints-cluster in region us-central1:
```
gcloud alpha admin-service-cluster instances create blueprints-cluster --location us-central1 --bundles Yakima
```

### Blueprints are incompatible with regular release of Kubernetes, delete and recreate a stable release
```
gcloud container clusters create krmapihost-blueprints-cluster \
    --release-channel stable \
    --addons ConfigConnector \
    --workload-pool=kasna-test-landingzone.svc.id.goog \
    --enable-stackdriver-kubernetes \
    --machine-type e2-standard-2 \
    --network default \
    --enable-vertical-pod-autoscaling \
    --region us-central1 \
    --num-nodes 2 \
    --node-locations us-central1-b,us-central1-c \
    --enable-autoscaling --min-nodes 1 --max-nodes 4 \
    --disk-size 10GB \
    --preemptible
```

### Enabling the Config Connector add-on:
```
gcloud container clusters update krmapihost-blueprints-cluster \
    --update-addons ConfigConnector=ENABLED --region=us-central1
```

### Create an IAM service account:
```
gcloud iam service-accounts create kix-blueprints
```

### Give the IAM service account elevated permissions:
```
gcloud projects add-iam-policy-binding kasna-test-landingzone \
    --member="serviceAccount:kix-blueprints@kasna-test-landingzone.iam.gserviceaccount.com" \
    --role="roles/owner"
```

### Create an IAM policy binding between the IAM service account and the predefined Kubernetes service account that Config Connector runs:
```
gcloud iam service-accounts add-iam-policy-binding kix-blueprints@kasna-test-landingzone.iam.gserviceaccount.com --member="serviceAccount:kasna-test-landingzone.svc.id.goog[cnrm-system/cnrm-controller-manager]" --role="roles/iam.workloadIdentityUser"
```

### Give Cloud Build permissions:
```
gcloud projects add-iam-policy-binding ${PROJECT_ID} --member=serviceAccount:${PROJECT_NUM}@cloudbuild.gserviceaccount.com --role=roles/container.clusterViewer
```

```
gcloud projects add-iam-policy-binding ${PROJECT_ID} --member=serviceAccount:${PROJECT_NUM}@cloudbuild.gserviceaccount.com --role=roles/container.developer
```

### Copy the following YAML file into a file named configconnector.yaml:

```yaml
# configconnector.yaml
apiVersion: core.cnrm.cloud.google.com/v1beta1
kind: ConfigConnector
metadata:
  # the name is restricted to ensure that there is only one
  # ConfigConnector resource installed in your cluster
  name: configconnector.core.cnrm.cloud.google.com
spec:
 mode: cluster
 googleServiceAccount: "kix-blueprints@kasna-test-landingzone.iam.gserviceaccount.com"
```

### Connect to GKE cluster:
```
gcloud container clusters get-credentials krmapihost-blueprints-cluster --region us-central1 --project $PROJECT_ID
```

### Namespace of config-controller-system:
```
kubectl create namespace config-controller-system
```

```
kubectl apply -f configconnector.yaml
```

```
kubectl annotate namespace config-controller-system cnrm.cloud.google.com/project-id=kasna-test-landingzone
```

### Remove the GKE cluster created by Blueprints Controller that hosts the Kubernetes API and Config Connector:
```
gcloud alpha admin-service-cluster instances delete blueprints-cluster --location us-central1 --project $PROJECT_ID
```

## You can now play with blueprints:
```
gcloud alpha blueprints apply --source=./network kasna-landing
```

```
gcloud alpha blueprints delete kasna-landing
```

```
kubectl api-resources --verbs=list --namespaced -o name | xargs -n 1 kubectl get --show-kind --ignore-not-found -n default
```

### Check the resources you have created:
```
gcloud compute instances list
```