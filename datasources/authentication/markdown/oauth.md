# OAuth 

OAuth is a standard for authentication which is used by many different services. It is a secure method of authentication which allows you to connect to a service without having to share your username and password.

## Setup

To setup OAuth you will need to create an application in the service you are connecting to. This will give you a client id and a client secret. You will need to enter these into the Datasource > Config UI.

### Authenticating with the service (data source)

When you click the authenticate button, you will be redirected to the service you are connecting to. You will be asked to login and then asked to grant access to the application you created in the setup step. Once you have granted access, you will be redirected back to the Datasource > Config UI.

The format of the URL will be similar to the following:

```text
https://{domain.com}/oauth2/auth?response_type=code&client_id={clientId}&redirect_uri=https%3A%2F%2Fapp.sharpsync.net%2Fdatasources%2Foauth%2Fcallback&scope={requiredScopes}&state={someValue}
```

where the following values are replaced:

* {domain.com} - the domain of the service you are connecting to
* {clientId} - the client id you created in the setup step
* {requiredScopes} - the scopes you require access to

## Troubleshooting
OAuth can return results which can be confusing for beginners. Below is a list of items which will help you troubleshoot your OAuth connection.

* invalid_request 
* invalid_grant

A result of `invalid_request` means that the client id or client secret is incorrect. You will need to check that you have entered the correct values into the Datasource > Config UI.

The error message returns a 400 Bad request with a body similar to:
```json
{
    "error": "invalid_request"
}
```


A result of `invalid_grant` means that:
* The code you received in the initial /GET request has expired or is incorrect. You will need to re-authenticate to get a new token.  OR
* The scopes you've used are incorrect or not matching with the scopes used when performing the initial /GET request in the browser

The error message returns a 400 Bad request with a body similar to:
```json
{
    "error": "invalid_grant"
}
```