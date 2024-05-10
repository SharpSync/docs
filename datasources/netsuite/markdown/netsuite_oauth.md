# NetSuite OAuth Setup

NOTES: 

1. In the setup steps below, the value of `{{netsuite-api}}` takes the form

> `https://{companyId}.suitetalk.api.netsuite.com`

2. In the setup steps below, the value of `{companyId}` is the numerical value of your company id

## Step: Create a new integration record

* Click Setup > Integration > Manage Integrations > New
* Enter a name for the integration
* Check the boxes for:
  * Authorization Code Grant
  * Restlets
  * Rest Web Services
* Get the consumer key (clientId) and consumer secret (client secret) - this will be used later.

## Step: Scopes

NetSuite requires that the following scopes are enabled for the OAuth connection to work:

* rest_webservices
* restlets (if you want to do thumbnail uploads this is required)

This forms part of the URL when performing the initial browser redirect

There are 3 steps to authenticating with NetSuite:
<ol>
  <li> A browser redirect
  <li> A call to the token endpoint to get the token
  <li> A call to refresh the token
</ol>

## Testing the OAuth setup
### Step: Browser redirect
Execute the following /GET request in a browser window

>https://`{companyId}`.app.netsuite.com/app/login/oauth2/authorize.nl?  
&nbsp;`response_type`=code&  
&nbsp;`client_id`={clientId}&  
&nbsp;`redirect_uri`=https://sharpsync.net/callback-oauth&  
&nbsp;`scope`=rest_webservices,restlets&  
&nbsp;`state`={someValue}

This will redirect to the login page for the NetSuite account. Once logged in, the user will be redirected to the redirect_uri (https://sharpsync.net) with the included state value.

>NOTE: The redirect_uri must be https://sharpsync.net/callback-oauth and must be url encoded (https%3A%2F%2Fsharpsync.net%2Fcallback-oauth)


### Step: Get the refresh token
When the previous /GET request is executed, the user will be redirected to the redirect_uri with a code value. This code value is used to get the refresh token.

Execute the following /POST request to the token endpoint. This should be made within 30 seconds of the previous step.

>`{{netsuite-api}}`/services/rest/auth/oauth2/v1/token

The body of the request should be:
* x-www-form-urlencoded
* include the following values:
  
>`grant_type`=authorization_code&  
`redirect_uri`=https%3A%2F%2Fsharpsync.net%2Fcallback-oauth&  
`code`={code}

The result of this request will look like this 

```json
{
    "access_token": "",
    "refresh_token": "",
    "expires_in": "3600",
    "token_type": "Bearer"
}
```

The important bit here is the `refresh_token`. We'll use it to get us a new `access_token` later.

### Step: Refresh the access token
Execute the following /POST request to the token endpoint. This should be made within 30 seconds of the previous step.

>`{{netsuite-api}}`/services/rest/auth/oauth2/v1/token

The body of the request should be:
* x-www-form-urlencoded
* include the following values:
  
>`grant_type`=authorization_code&  
`redirect_uri`=https%3A%2F%2Fsharpsync.net%2Fcallback-oauth&  
`refresh_token`={refresh-token}

The result will look like this

```json
{
    "access_token": "",
    "expires_in": "3600",
    "token_type": "Bearer"
}
```

The important bit here is the `access_token` which gives us access to NetSuite.

Your preparation is now ready and you can move on to configuring NetSuite as a datasource

