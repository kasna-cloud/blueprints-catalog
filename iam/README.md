# Background

1. create service account in project, and grant a specific member a role (default to roles/iam.serviceAccountKeyAdmin) for accessing the service account that just created.
2. Grant user permission to specified role
3. Grant service account permission to specified role


# Usage

  ```
  kpt cfg set . project-id kasna-test-landingzone
  kpt cfg set . service-account-name service-account-cloudsql
  kpt cfg set . iam-member user:sam.gh.lin@kasna.com.au
  kpt cfg set . role roles/cloudsql.admin
  ```

  You can check the resources you just created:

  ```
  kubectl get iamserviceaccount --namespace config-controller-system
  kubectl get iampolicymember --namespace config-controller-system
  ```
