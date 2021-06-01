## Resource Input

### Bucket

- name
- location_type (multi-region, dual-region, **region**)
- location (https://cloud.google.com/compute/docs/regions-zones#available, **australia-southeast1**)
- storage_class (**standard**, nearline, coldline, archive)
- access_control (**uniform**, fine-grained)

https://cloud.google.com/storage/docs/creating-buckets

### CloudSQL

- engine (**PostgreSQL**/MySQL/SQL Server)
- instance_id
- database_version
- region
- zone_availability (single/**multiple**)
  - primary_zone (multiple)
  - secondary_zone (multiple)
- machine_type
  - cores (1-1000)
  - memory (3.75-13)
- storage_type (**ssd**, hdd)
- storage_capacity (10-30,720)
- connections (public/**private**) 


https://cloud.google.com/sdk/gcloud/reference/sql/instances/create  

### Cloudrun

- name
- region
- cloud_build_integration (boolean)
  - source_repository (true)
  - container_image (false)
- container_port
- container_command
- container_arguments
- cores (1-4)
- memory
- request_timeout
- max_requests
- min_instance
- max_instance
  

### GKE

- name
- location_type (**regional**)
  - region (**australia-southeast1**)
- version_channel (**regular**, rapid, stable)
- version (filtered by **version_channel** type)
- network
- subnetwork
- features
 - istio (boolean)
- node_pools (tbc) 

### Monitoring

get simple monitoring dashboard running
