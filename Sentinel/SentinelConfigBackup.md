# Azure Sentinel Configuration Backup

This Logic App allows you to export the Azure Sentinel configuration. Every operation group are exported via API REST to a JSON file, with all configuration parameters.

These JSON files are stored in a Storage Account, by date.

[SentinelConfigBackup.json](SentinelConfigBackup.json)


## API Version

The Sentinal service has changed over time. There are new and changed operations groups.

This Logic App is based on [API version](https://docs.microsoft.com/en-us/rest/api/securityinsights/api-versions) 2021-09-01-preview

## Permissions

It's convenient to configure a Service Principal in Azure AD to make calls to the Azure API REST, instead of a user. This Enterprise Application must have 'user_impersonation' permissions and the necessary IAM permission per RBAC on each subscription or resource group where you where it will run.

Only Reader role are needed on Sentinel Subscription.


## Customise parameters

This following values should be customised in the Logic App json file, with your personal data about the Service Principal to make calls to the API and values of Sentinel subscription.

```
_LOG_ANALYTICS_WORKSPACE_SENTINEL_SUBSCRIPTION_ID_
_LOG_ANALYTICS_WORKSPACE_SENTINEL_RESOURCE_GROUP_NAME_
_LOG_ANALYTICS_WORKSPACE_SENTINEL_NAME_
_SERVICE_PRINCIPAL_TENANT_ID_
_SERVICE_PRINCIPAL_CLIENT_ID_
_SERVICE_PRINCIPAL_CLIENT_SECRET_ID_
```

Also, the Storage Account Resource ID, and particularly the resource location, should be checked:

`"/subscriptions/_LOG_ANALYTICS_WORKSPACE_SENTINEL_SUBSCRIPTION_ID_/providers/Microsoft.Web/locations/westeurope/managedApis/azureblob"`
