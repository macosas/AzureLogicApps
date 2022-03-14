# Newly Azure Resources created

This Logic App allows you to add a new IP to Block List in a Named Location of the Azure Conditional Access. This app use Update method of Graph Api Rest to refresh the list entirely, reading the actual ip's configure it and adding the new one 'IPtoBlock' variable.

The Named Location must already exist, and be passed as an argument to the API REST call.

It's mandatory adjusts the customise parameters, like the Named Location ID to update with a New IP with Subnet Mask value.

[BlockIPsCA.json](BlockIPsCA.json)



## Permissions

It's convenient to configure a Service Principal in Azure AD to make calls to the Azure API REST, instead of a user. This Enterprise Application must have 'user_impersonation' and one of the following permissions is required to call this API:

- Delegated (work or school account)
	- Policy.Read.All
	- Policy.ReadWrite.ConditionalAccess
- Delegated (personal Microsoft account)
	- Not supported.
- Application
	- Policy.Read.All
	- Policy.ReadWrite.ConditionalAccess



## Customise parameters

This following values should be customised in the Logic App json file, with your personal data about the Service Principal to use Graph API REST.

```
_NAMED_LOCATION_ID_
_NEW_IP_AND_SUBNET_MASK_
_SERVICE_PRINCIPAL_TENANT_ID_
_SERVICE_PRINCIPAL_CLIENT_ID_
_SERVICE_PRINCIPAL_CLIENT_SECRET_ID_
```


## Documentation

- [API REST Update ipNamedlocation](https://docs.microsoft.com/en-us/graph/api/ipnamedlocation-update?view=graph-rest-beta&tabs=http)
- [How to convert string variable to valid json]( https://social.msdn.microsoft.com/Forums/en-US/14b2af82-d987-4de2-a00e-98cdb8a052b3/how-to-convert-string-variable-to-valid-json)
- [Store and manage values by using variables in Azure Logic Apps](https://docs.microsoft.com/en-us/azure/logic-apps/logic-apps-create-variables-store-values)
