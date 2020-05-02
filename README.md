# azuread-oauth-controller-demo
A demonostration of using AzureAd app registrations to get a token (client side) and authenticate the token (server side).

# Requirements
1. Create two new App registrations via Azure Portal. Call one server and the other consumer.
2. In the server app registration go to Manage > Manifest and add a role
```json
...
"appRoles": [
  {
    "allowedMemberTypes": [
      "Application"
    ],
    "description": "Consumer apps have access to the consumer data.",
    "displayName": "ConsumerApps",
    "id": "ccf784a6-fd0c-45f2-9c08-2f9d162a0628",
    "isEnabled": true,
    "lang": null,
    "origin": "Application",
    "value": "demo:get"
  }
],
...
```
3. In the client app registration assign a permission to the role we added, Manage > API permissions > Add Permission > My APIs.
4. Load and use the postman collection to get a token and call against the controller.

# References
1. [A web API that calls web APIs](https://docs.microsoft.com/en-us/azure/active-directory/develop/scenario-web-api-call-api-overview)
