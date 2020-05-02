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

# Troubleshooting
If you are receiving 401 or 403, ensure the access token has the role we assigned earlier, inspect with [jwt.io](https://jwt.io/), e.g.:
```json
{
  "aud": "api://e7f9502f-a27f-40ab-a9b6-a59a371e0dbd",
  "iss": "https://sts.windows.net/f30bb8e3-9db6-4d44-b3ae-67fa5864b725/",
  "iat": 1588381888,
  "nbf": 1588381888,
  "exp": 1588385788,
  "aio": "42dgYChbseicQazs6xMlUlfba7YcBQA=",
  "appid": "ebf09f5d-79d0-43ab-91ff-aa4e2bc33e5a",
  "appidacr": "1",
  "idp": "https://sts.windows.net/f30bb8e3-9db6-4d44-b3ae-67fa5864b725/",
  "oid": "689902c6-8d36-4cd8-97b2-5e4f97c03a77",
  "roles": [
    "demo:get"
  ],
  "sub": "689902c6-8d36-4cd8-97b2-5e4f97c03a77",
  "tid": "f30bb8e3-9db6-4d44-b3ae-67fa5864b725",
  "uti": "w8te0DxQLke60m_9NfnHAA",
  "ver": "1.0"
}
```

# References
1. [A web API that calls web APIs](https://docs.microsoft.com/en-us/azure/active-directory/develop/scenario-web-api-call-api-overview)
