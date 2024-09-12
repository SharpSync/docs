# NetSuite OAuth Setup

 * [Create a new integration record](#create-a-new-integration-record)
 * [Permissions](#permissions)
 * [Scopes](#scopes)

NOTES: 

1. In the setup steps below, the value of `{{netsuite-api}}` takes the form

> `https://{companyId}.suitetalk.api.netsuite.com`

2. In the setup steps below, the value of `{companyId}` is the numerical value of your company id
3. You need the permission `Permissions > Setup > Access Token Management` to make `Integration Record` changes
## Step: Create a new integration record

For this to happen you need the permissions 
* Lists > Integration application and
* Setup > Integration Application permissions 

To create a new integration record do the following:

* Click Setup > Integration > Manage Integrations > New
* Enter a name for the integration
* Check the boxes for:
  * Authorization Code Grant
  * Restlets
  * Rest Web Services
* Get the consumer key (clientId) and consumer secret (client secret) - this will be used later.

Make sure to tick `Ask first time` under `OAUTH 2.0 CONSENT POLICY`

## Step: Permissions

  Permissions Required for NetSuite Integration role

 ### Under Setup -> Records Catalogue 
 Search for a record you need, then click on the "SuiteScript and REST Query API"

 Navigate to the role you want to assign the permissions to, and add the following permissions:
  
 > Setup > Roles > Manage Roles > Developer
(Or whichever role you want to assign the permissions to)
 

| Section                    | Functionality                  | Access |
|----------------------------|--------------------------------|--------|
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
| Permissions > Lists        | Locations                      | Full   |
| Permissions > Lists        | Manufacturing Routing          | Full   |
| Permissions > Lists        | Perform Search                 | Full   |
| Permissions > Lists        | Product Classes                | Full   |
| Permissions > Lists        | Subsidiaries                   | Full   |
| Permissions > Lists        | Tax Schedules                  | View   |
| Permissions > Lists        | Units                          | View   |
| Permissions > Lists        | Vendors                        | View   |
| Permissions > Setup        | Allows JS / HTML uploads       | Full   |
| Permissions > Setup        | Custom Item fields             | Full   |
| Permissions > Setup        | Custom Number Item fields      | Full   |
| Permissions > Setup        | Custom Lists                   | Full   |
| Permissions > Setup        | Custom Sublist                 | Full   |
| Permissions > Setup        | Custom Sublists                | Full   |
| Permissions > Setup        | Login using Access Tokens      | Full   |
| Permissions > Setup        | Login using OAuth 2.0 Tokens   | Full   |
| Permissions > Setup        | REST Web Services              | Full   |
| Permissions > Setup        | SuiteScript                    | Full   |
| Permissions > Setup        | SuiteApp Deployment            | Full   |
| Permissions > Setup        | View Login Audit Trail         | Full   |
| Permissions > Reports      | SuiteAnalytics Workbook        | Edit   |
| Forms > Item               | Group/Kit/Assembly             | Enabled|
| Forms > Item               | Inventory Part                 | Enabled|
| Forms > Item               | Non-Inventory Part             | Enabled|
| Forms > Inventory Detail   | Inventory Detail               | Enabled|
| Forms > Other record       | Item Location                  | Enabled|
| Forms > Other record       | Manufacturing Routing          | Enabled|
  
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

