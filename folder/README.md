# Google folder, project blueprint
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
gcloud projects add-iam-policy-binding ${PROJECT_ID} --member=serviceAccount:${PROJECT_NUM}@cloudbuild.gserviceaccount.com --role=roles/resourcemanager.folderCreator
```
- Folder Editor
```
gcloud projects add-iam-policy-binding ${PROJECT_ID} --member=serviceAccount:${PROJECT_NUM}@cloudbuild.gserviceaccount.com --role=roles/resourcemanager.folderEditor
```
- Project Creator
```
gcloud projects add-iam-policy-binding ${PROJECT_ID} --member=serviceAccount:${PROJECT_NUM}@cloudbuild.gserviceaccount.com --role=roles/resourcemanager.projectCreator
```
- Project Deleter
```
gcloud projects add-iam-policy-binding ${PROJECT_ID} --member=serviceAccount:${PROJECT_NUM}@cloudbuild.gserviceaccount.com --role=roles/resourcemanager.projectDeleter
```

Bind `Billing Account User` IAM role to service-[PROJECT_NUMBER]@gcp-sa-[PREVIEW_PRODUCT].iam.gserviceaccount.com