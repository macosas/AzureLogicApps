# Newly Azure Resources created

This Logic App allows you to lookup the AzureActivity logs to get the new Azure resources. And also the updated resources. This query contains exclusions that you can customise, so that you get as little noise as possible in your report.

I use an Azure Graph loop to get the name of the Subscription from the SubscriptionID.

The Logic App run daily at 1PM sending an email with a list of resources. If there is nothing new in the subscriptions, it will not send the mail.

[NewAzResourcesCreated.json](NewAzResourcesCreated.json)



## Permissions

It's convenient to configure a Service Principal in Azure AD to make calls to the Azure API REST, instead of a user. This Enterprise Application must have 'user_impersonation' permissions and Reader role are needed on Sentinel Subscription.

An AD user must be configured for email sending and validated in the Office365 connector.


## Customise parameters

This following values should be customised in the Logic App json file, with your personal data about the Service Principal to make calls to the API and values of Sentinel subscription.

```
_EMAIL_ACCOUNTS_SEPARATED_BY_SEMICOLON_
_OFFICE365_CONNNECTION_NAME_
_MONITOR_CONNECTION_NAME_
_LOG_ANALYTICS_WORKSPACE_SENTINEL_SUBSCRIPTION_ID_
_LOG_ANALYTICS_WORKSPACE_SENTINEL_RESOURCE_GROUP_NAME_
_LOG_ANALYTICS_WORKSPACE_SENTINEL_NAME_
_SERVICE_PRINCIPAL_TENANT_ID_
_SERVICE_PRINCIPAL_CLIENT_ID_
_SERVICE_PRINCIPAL_CLIENT_SECRET_ID_
```
