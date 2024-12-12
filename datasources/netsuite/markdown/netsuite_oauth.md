# NetSuite OAuth Setup

NetSuite supports industry standard OAuth authentication and authorization. The implementation in SharpSync uses OAuth2 exclusively at this point. Should you require a different implementation such as API keys or OAuth1.0, please engage us

 * [Create a new integration record](#step-create-a-new-integration-record)
 * [Scopes](#step-scopes)
 * [Permissions](#step-permissions)
 * [Testing the OAuth setup](#testing-the-oauth-setup)

NOTES: 

1. In the setup steps below, the value of `{{netsuite-api}}` takes the form

> `https://{companyId}.suitetalk.api.netsuite.com`

2. In the setup steps below, the value of `{companyId}` is the numerical value of your company id
3. You need the permission `Permissions > Setup > Access Token Management` to make `Integration Record` changes
## Step: Create a new integration record

For this to happen you need the permissions 
* Lists > Integration application and
* Setup > Integration Application 

To create a new integration record do the following:

* Click Setup > Integration > Manage Integrations > New
* Enter a name for the integration
* Check the boxes for:
  * Authorization Code Grant
  * Restlets
  * Rest Web Services
* Get the consumer key (clientId) and consumer secret (client secret) - this will be used later.

Make sure to tick `Ask first time` under `OAUTH 2.0 CONSENT POLICY`

## Step: Scopes

NetSuite requires that the OAuthe flow uses the following scopes. Ensure they are enabled for the OAuth connection to work:

* rest_webservices
* restlets

This forms part of the URL when performing the initial browser redirect

There are 3 steps to authenticating with NetSuite using OAuth:

* A browser redirect
* A call to the token endpoint to get the token
* A call to refresh the token

For the first 2 steps the OAuth client id and secret is required.  If successful, you'll be issued an access token. For the last step the refresh token is required to renew your access token

## Step: Permissions

  Permissions Required for NetSuite Integration role. These permissions are quired for the successful setup of SharpSync. Some of the permissions are not required for your users (the role your users will be logging in with), and are marked as `Setup Only` below. Once all the permissions has been setup, make sure to [test the setup](#testing-the-oauth-setup)

 ### Under Setup -> Records Catalogue 
 Search for a record you need, then click on the "SuiteScript and REST Query API"

 Navigate to the role you want to assign the permissions to, and add the following permissions:
  
 > Setup > Roles > Manage Roles > Developer
(Or whichever role you want to assign the permissions to)
 

| Section                    | Functionality                  | Access | Required |
|----------------------------|--------------------------------|--------| -------- |
| Permissions > Transactions | Audit Trail                    | View   |
| Permissions > Transactions | Find Transaction               | View   |
| Permissions > Transactions | Receive Inventory              | View   |
| Permissions > Transactions | Sales Order                    | View   |
| Permissions > Reports      | SuiteAnalytics Workbook        | Edit   |
| Permissions > Lists        | Accounts                       | View   |
| Permissions > Lists        | Address list in Search         | View   |
| Permissions > Lists        | Bill of Materials              | Full   |
| Permissions > Lists        | Cost of Goods Sold Registers   | View   |
| Permissions > Lists        | Departments                    | View   |
| Permissions > Lists        | Documents and Files            | Full   |
| Permissions > Lists        | Employee Record                | View   |
| Permissions > Lists        | Employees                      | View   |
| Permissions > Lists        | Items                          | Full   |
| Permissions > Lists        | Locations                      | View   |
| Permissions > Lists        | Manufacturing Routing          | Full   |
| Permissions > Lists        | Manufacturing Cost Template    | View   | Optional |
| Permissions > Lists        | Perform Search                 | Full   |
| Permissions > Lists        | Product Classes                | Full   |
| Permissions > Lists        | Subsidiaries                   | View   |
| Permissions > Lists        | Tax Schedules                  | View   |
| Permissions > Lists        | Tax Records                    | View   |
| Permissions > Lists        | Units                          | View   |
| Permissions > Lists        | Vendors                        | View   |
| Permissions > Setup        | Allows JS / HTML uploads       | Full   | Setup Only |
| Permissions > Setup        | Custom Item fields             | Full   | Setup Only |
| Permissions > Setup        | Custom Number Item fields      | Full   | Setup Only |
| Permissions > Setup        | Custom Lists                   | Full   | Setup Only |
| Permissions > Setup        | Custom Sublist                 | Full   | Setup Only |
| Permissions > Setup        | Custom Sublists                | Full   | Setup Only |
| Permissions > Setup        | Login using Access Tokens      | Full   | Setup Only |
| Permissions > Setup        | Login using OAuth 2.0 Tokens   | Full   | Setup Only |
| Permissions > Setup        | REST Web Services              | Full   | Setup Only |
| Permissions > Setup        | SuiteScript                    | Full   | Setup Only |
| Permissions > Setup        | SuiteApp Deployment            | Full   | Setup Only |
| Permissions > Setup        | View Login Audit Trail         | Full   | Setup Only |
| Permissions > Reports      | SuiteAnalytics Workbook        | Edit   |
| Forms > Item               | Group/Kit/Assembly             | Enabled|
| Forms > Item               | Inventory Part                 | Enabled|
| Forms > Item               | Non-Inventory Part             | Enabled|
| Forms > Inventory Detail   | Inventory Detail               | Enabled|
| Forms > Other record       | Item Location                  | Enabled|
| Forms > Other record       | Manufacturing Routing          | Enabled|
  

## Testing the OAuth setup

### Step: Browser redirect

Execute the following /GET request in a browser window.

>https://`{companyId}`.app.netsuite.com/app/login/oauth2/authorize.nl?  
&nbsp;`response_type`=code&  
&nbsp;`client_id`={clientId}&  
&nbsp;`redirect_uri`=https://sharpsync.net/callback-oauth&  
&nbsp;`scope`=rest_webservices,restlets&  
&nbsp;`state`={someValue}

This will redirect to the login page for the NetSuite account. Once logged in, the user will be redirected to the redirect_uri (https://sharpsync.net) with the included state value.

>NOTE: The redirect_uri must be https://sharpsync.net/callback-oauth and must be url encoded (https%3A%2F%2Fsharpsync.net%2Fcallback-oauth)

If this step is successful, you'll see the login window and a code at the end of the URL displayed in the browser.

### Step: Get the refresh token

When the previous /GET request is executed, the user will be redirected to the `redirect_uri` with a code value. This code value is used to get the refresh token as well as a new access token.

Some terminology:
* `code` - issued by the OAuth 2 authentication cycle. Used to get the initial `access_token` and `refresh_token`
* `access_token` - let's you access resources in NetSuite. Expires after about an hour
* `refresh_token` - let's you get a new `access_token` repeatedly

<span style='color:orange'> You should treat an access token and a refresh token the same as a username and password! It is sensitive information</span>

Execute the following /POST request to the token endpoint. This should be made within 30 seconds of the previous step. (Note that we're now using the `.suitetalk.api` subdomain)

>https://`{companyId}`.suitetalk.api.netsuite.com/services/rest/auth/oauth2/v1/token

The body of the request should be:
* x-www-form-urlencoded
* include the following values:
  
>`grant_type`=authorization_code&  
`redirect_uri`=https%3A%2F%2Fsharpsync.net%2Fcallback-oauth&  
`code`={code}

The result of this request will look like this  (`refresh_token` AND `access_token`)

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

>https://`{companyId}`.suitetalk.api.netsuite.com/services/rest/auth/oauth2/v1/token

The body of the request should be:
* x-www-form-urlencoded
* include the following values:
  
>`grant_type`=authorization_code&  
`redirect_uri`=https%3A%2F%2Fsharpsync.net%2Fcallback-oauth&  
`refresh_token`={refresh-token}

The result will look like this (no `refresh_token`, only the `access_token`)

```json
{
    "access_token": "",
    "expires_in": "3600",
    "token_type": "Bearer"
}
```

The important bit here is the `access_token` which gives us access to NetSuite.

Your preparation is now ready and you can move on to configuring NetSuite as a datasource

