## Resource structure
```
blueprints
├── README.md
├── folders
│   ├── Kptfile
│   ├── README.md
│   ├── folder.yaml
│   └── setters.yaml
├── projects
│   ├── Kptfile
│   ├── dns.yaml
│   ├── firewall.yaml
│   ├── gke.yaml
│   ├── network.yaml
│   ├── project.yaml
│   ├── pubsub-sub.yaml
│   ├── service_account.yaml
│   ├── service_apis.yaml
│   └── setters.yaml
└── support
    ├── Kptfile
    ├── project.yaml
    ├── pubsub.yaml
    ├── service_account.yaml
    └── setters.yaml
```

## Resources

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:--------:|
| active\_apis | The list of active apis on the service project. If api is not active this module will not try to activate it | `list(string)` | `[]` | no |
| enable\_shared\_vpc\_service\_project | Flag set if SVPC enabled | `bool` | n/a | yes |
| grant\_services\_security\_admin\_role | Whether or not to grant Kubernetes Engine Service Agent the Security Admin role on the host project so it can manage firewall rules | `bool` | `false` | no |
| host\_project\_id | The ID of the host project which hosts the shared VPC | `string` | n/a | yes |
| lookup\_project\_numbers | Whether to look up the project numbers from data sources. If false, `service_project_number` will be used instead. | `bool` | `true` | no |
| service\_project\_id | The ID of the service project | `string` | n/a | yes |
| service\_project\_number | Project number of the service project. Will be used if `lookup_service_project_number` is false. | `string` | `null` | no |
| shared\_vpc\_subnets | List of subnets fully qualified subnet IDs (ie. projects/$project\_id/regions/$region/subnetworks/$subnet\_id) | `list(string)` | `[]` | no |