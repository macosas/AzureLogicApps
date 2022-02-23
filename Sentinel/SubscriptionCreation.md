# Monitoring for Azure Subscription Creation

An easy approach to watch a new Azure Subscription is with a Logic App, using the List Subscriptions connector from Azure Resource Manager.

The event will send to a Custom Log table on Log Analytics Workspace of Sentinel. Once we have the data in Log Analytics we can either visualize new subscriptions or alert on them. Also, an email will send to Security Cloud managers.


[SubscriptionCreation.json](SubscriptionCreation.json)



## Permissions

It's convenient to configure a Service Principal in Azure AD to make calls to the Azure API REST, instead of a user. This Enterprise Application must have 'user_impersonation' permissions. The Service Principal need Reader role RBAC on every Subscription.

You need the Service Principal tenant ID, client ID and client secret ID data to configure the Azure Resource Manager connector.



## Custom Log Sentinel

Run the Logic App one time before to create this Custom Log. The JSON data obtained is useful to create this Custom Log uploading this file.

Custom Log name: **SubscriptionInventory_CL**

Sentinel query:
```
SubscriptionInventory_CL 
| summarize arg_min(TimeGenerated, *) by SubscriptionId 
| where TimeGenerated >= ago(4h) 
| project TimeGenerated, displayName_s, state_s, SubscriptionId 
```


## Customise parameters

This following values should be customised in the Logic App json file, with your personal data about the Service Principal to make calls to the API and values of Sentinel subscription.

```
_LOG_ANALYTICS_WORKSPACE_SENTINEL_SUBSCRIPTION_ID_
_LOG_ANALYTICS_WORKSPACE_SENTINEL_RESOURCE_GROUP_NAME_
```

Also, the resource location for Storage Account Resource ID should be checked:

`providers/Microsoft.Web/locations/westeurope/`





## Documentation

- [Original documentation of Microsoft Tech Community](https://techcommunity.microsoft.com/t5/core-infrastructure-and-security/monitoring-for-azure-subscription-creation/ba-p/2018879)
