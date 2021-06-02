# Background

create service account in project, and grant a specific member a role (default to roles/iam.serviceAccountKeyAdmin) for accessing the service account that just created.


# Usage

  ```
  kpt cfg set . iam-member user:samuel.lin@kasna.com.au
  ```

  You can check the resources you just created:

  ```
  kubectl get iamserviceaccount --namespace config-controller-system
  kubectl get iampolicymember --namespace config-controller-system
  ```
