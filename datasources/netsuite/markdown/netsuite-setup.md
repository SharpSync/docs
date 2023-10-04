# NetSuite Setup

Steps involved in setting up NetSuite:
* Setup an upload folder (optional)
* Setup restlet for uploading thumbnails (optional - goes with previous step)
* Setup OAuth

## Setup the upload folder
Updating thumbnails in NetSuite requires the usage of an external restlet. The restlet used was developed by Tim Dietrich and is freely available at https://suiteapi.com. This is optional but highly recommended.

Steps required:
* Create a new folder in NetSuite
* Navigate to latest version of  [SuiteAPI](https://suiteapi.com)
* [Download](https://tdietrich-opensource.s3.amazonaws.com/suitescripts/SuiteAPI-v2022.1.zip) the SuiteApi zip file for the restlet
* Install using the [instructions](https://suiteapi.com/documentation/) on the site <sup>**</sup>


** At the time of writing the documentation was available. If the above link / website cannot be found, a copy (current at the time of writing) of the file and the instructions can be found using the link below:

### Step: Create a new thumbnails folder in NetSuite
 
* Navigate to NetSuite
* Click on the `Documents` menu item
* Click on the `Files` sub menu item > File Cabinet
* Click on the `New Folder` button
  * Folder name: `SharpSync`
  * Subfolder of: nothing
  * Type `Documents and Files`
  * Click `Save`
* Click on the `New Folder` button again
  * Folder name: `Thumbnails`
  * Subfolder of: `SharpSync`
  * Type `Documents and Files`
  * Click `Save`

With this last folder selected in the file cabinet, take note of the folder id in the URL. This will be used later. The url at the top will look something like this:

> https://`{companyId}`.app.netsuite.com/app/common/media/mediaitemfolders.nl?`folder=20149768`&whence=&cmid=...
  
## Upload SuiteApi
If for some reason the website is unavailable, a copy of the Suite API zip file can be found here: [SuiteAPI-v2022.1.zip](SuiteApi.v2022.1.zip)
Follow the steps in the SuiteApi setup 
## Setup OAuth

 NOTE: In the OAuth setup steps below, the value of `{{netsuite-api}}` takes the form 

> `https://{companyId}.suitetalk.api.netsuite.com`

### Step: Create a new integration record

* Click Setup > Integration > Manage Integrations > New
* Enter a name for the integration
* Check the boxes for:
  * Authorization Code Grant
  * Restlets
  * Rest Web Services

### Step: Scopes

NetSuite requires that the following scopes are enabled for the OAuth connection to work:

* rest_webservices
* restlets

This forms part of the URL when performing the initial browser redirect

There are 3 steps to authenticating with NetSuite:
<ol>
  <li> A browser redirect
  <li> A call to the token endpoint to get the token
  <li> A call to refresh the token
</ol>

### Testing the setup
#### Step: Browser redirect
Execute the following /GET request in a browser window

>https://`{companyId}`.app.netsuite.com/app/login/oauth2/authorize.nl?  
&nbsp;`response_type`=code&  
&nbsp;`client_id`={clientId}&  
&nbsp;`redirect_uri`=https://sharpsync.net/callback-oauth&  
&nbsp;`scope`=rest_webservices,restlets&  
&nbsp;`state`={someValue}

This will redirect to the login page for the NetSuite account. Once logged in, the user will be redirected to the redirect_uri (https://sharpsync.net) with the included state value.

>NOTE: The redirect_uri must be https://sharpsync.net/callback-oauth and must be url encoded (https%3A%2F%2Fsharpsync.net%2Fcallback-oauth)


#### Step: Get the refresh token
When the previous /GET request is executed, the user will be redirected to the redirect_uri with a code value. This code value is used to get the refresh token.

Execute the following /POST request to the token endpoint. This should be made within 30 seconds of the previous step.

>`{{netsuite-api}}`/services/rest/auth/oauth2/v1/token

The body of the request should be:
* x-www-form-urlencoded
* include the following values:
  
>`grant_type`=authorization_code&  
`redirect_uri`=https%3A%2F%2Fsharpsync.net%2Fcallback-oauth&  
`code`={code}

#### Step: Refresh the access token
Execute the following /POST request to the token endpoint. This should be made within 30 secondns of the previous step.

>`{{netsuite-api}}`/services/rest/auth/oauth2/v1/token

The body of the request should be:
* x-www-form-urlencoded
* include the following values:
  
>`grant_type`=authorization_code&  
`redirect_uri`=https%3A%2F%2Fsharpsync.net%2Fcallback-oauth&  
`refresh_token`={refresh-token}

## Putting it all together 

With the copied URL in the previous step, and the folder Id from the first step, it's time to setup the datasource in SharpSync. In SharpSync add a new data source > NetSuite

### Configuring NetSuite

There are 2 configuration sections for each datasource
* Authentication
* BOM Configuration

#### Authentication
* Navigate to the Datasources > Config UI
* Select the NetSuite datasource
* Enter the following values:
  
  |Name|Description|Recommended value|
  |--|--|--|
  |Base API Path|The location where data is pulled from|https://{companyId}.suitetalk.api.netsuite.com|
  |Authentication Type|Which authentication method you'd like to use to connect to NetSuite|OAuth 2.0|
  |OAuth Url|The URL against which your OAuth authentication occurs|https://{companyId}.app.netsuite.com/app/login/oauth2/authorize.nl|
  |OAuth Token Url|The URL against which your OAuth token is refreshed|https://{companyId}.suitetalk.api.netsuite.com/services/rest/auth/oauth2/v1/token|
  |Client Id|The client id generated by the integration record created|-|
  |Client Secret|The client secrete generated by the integration record created|-|
  |OAuth Scopes|The scopes required to get data. The `restlets` scope is optional but highly recommended. Without it you will not be able to upload thumbnails|rest_webservices,restlets|
  

#### BOM Configuration
  |Name|Description|Recommended value|
  |--|--|--|
  |Top level assembly column name|When querying the data you may use this value to identify assemblies (optional)|itemid|
  |SuiteQL BOM Query|The query used to select data using SuiteQl|`SELECT ItemID, id, displayName FROM Item WHERE ItemID = '{uniquePartNumber}'`. Note that the place holder `{uniquePartNumber}` must stay as this is used to find items related to assemblies |
  |Servlet URL|The url of the servlet where thumbnails will be uploaded. Optional but recommented. If specified, include the `folderId` param at the end|https://{companyId}.restlets.api.netsuite.com/app/site/hosting/restlet.nl?script=2943&deploy=1&folderId={folderId}|
  |Thumbnail column name|The column to update in NetSuite using the file ID of the uploaded thumbnail|custitem_mycol_image|
  

* Enter the URL of the restlet, followed by `&folderId=` and the id of the folder in the first steps
* Enter the folder ID into the UI in the form
 
> `{{netsuite-api}}`/app/site/hosting/restlet.nl?script={yourScriptId}&deploy=1&folderId={folderId}

e.g.

> `{{netsuite-api}}`/app/site/hosting/restlet.nl?script=`2743`&deploy=1&folderId=`19578359`


See also 

* [OAuth](../../authentication/markdown/oauth.md)