# logging-sink blueprint

1. Creates logging-sink
2. Creates sms notification channel to send notification to number X 
3. Creates monitoring policy to send alert to above sms notification channel when instance CPU usage is over 90%

# Usage

Set required variables

```
kpt cfg set . billing-id 014244-F1A39A-218EB5
kpt cfg set . sms-number 61430448123
```

Run blueprint apply

```
gcloud alpha blueprints apply --source=./sre monitoring-and-logging
```

You can check the resources you just created:

```
kubectl get LoggingLogSink --namespace config-controller-system
kubectl get MonitoringNotificationChannel --namespace config-controller-system
kubectl get LoggingLogSink --namespace config-controller-system
```

# View in console

[Monitoring Policy](https://console.cloud.google.com/monitoring/alerting/policies?orgonly=true&project=kasna-test-landingzone&supportedpurview=organizationId)

[Notification Channel](https://console.cloud.google.com/monitoring/alerting/notifications?orgonly=true&project=kasna-test-landingzone&supportedpurview=organizationId)