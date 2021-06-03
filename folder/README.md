# WIP - Google folder, project blueprint
This blueprint creates a folder and a project in it

## Replace the following in Kptfile:
- ${FOLDER_NAME}
- ${PROJECT_ID}
- ${PARENT_FOLDER_ID} is the parent folder to create a folder under, requires quotes otherwise apply command will fail to parse as string
- ${BILLING_ACCOUNT_ID}

## Create the following IAM role binding 
${PARENT_FOLDER_ID} can be in a different organization. Bind the following IAM roles to
service-[PROJECT_NUMBER]@gcp-sa-[PREVIEW_PRODUCT].iam.gserviceaccount.com:

- Folder Creator
```
gcloud projects add-iam-policy-binding ${PROJECT_ID} --role=roles/resourcemanager.folderCreator --condition=None --member="serviceAccount:kasna-test-landingzone.svc.id.goog[cnrm-system/cnrm-controller-manager]"
```
- Folder Editor
```
gcloud projects add-iam-policy-binding ${PROJECT_ID} --role=roles/resourcemanager.folderEditor --condition=None --member="serviceAccount:kasna-test-landingzone.svc.id.goog[cnrm-system/cnrm-controller-manager]"
```
- Project Creator
```
gcloud projects add-iam-policy-binding ${PROJECT_ID} --role=roles/resourcemanager.projectCreator --condition=None --member="serviceAccount:service-915663602069@gcp-sa-yakima.iam.gserviceaccount.com"
```
- Project Deleter
```
gcloud projects add-iam-policy-binding ${PROJECT_ID} --role=roles/resourcemanager.projectDeleter --condition=None --member="serviceAccount:kasna-test-landingzone.svc.id.goog[cnrm-system/cnrm-controller-manager]"
```

Bind `Billing Account User` IAM role to service-[PROJECT_NUMBER]@gcp-sa-[PREVIEW_PRODUCT].iam.gserviceaccount.com