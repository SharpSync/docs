# NetSuite Setup of Thumbnail foler

To successfully upload thumbnails to NetSuite, you need the following 3 things:
* OAuth `clientId` and `clientSecret` (aka consumer key and consumer secret)
* A `scriptId`
* A `folderId`


Steps involved in setting up NetSuite:
* [Setup OAuth](#setup-oauth) - gives you permissions to upload files +  `clientId` and `clientSecret`
* [Setup restlet for uploading thumbnails (SuiteApi)](#setup-restlet-for-uploading-thumbnails-suiteapi) - gives you the `scriptId`
* [Setup an upload folder](#setup-an-upload-folder) - gives you the `folderId`
* [Putting it all together](#putting-it-all-together) - configuring the datasource in SharpSync

<hr />

## Setup OAuth

**Goal**: To get the the necessary permissions to upload files


Steps required:

* (done) Install SuiteApi
* Setup OAuth (this step)
* Setup SuiteApi
* Create a new thumbnails folder in NetSuite
* Setup the datasource to point to the new restlet


 NOTE: In the OAuth setup steps below, the value of `{{netsuite-api}}` takes the form 

> `https://{companyId}.suitetalk.api.netsuite.com`

### Step: Create a new integration record

* Click Setup > Integration > Manage Integrations > New
* Enter a name for the integration
* Check the boxes for:
  * Authorization Code Grant
  * Restlets
  * Rest Web Services
* Get the consumer key (clientId) and consumer secret (client secret) - this will be used later.

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

### Testing the OAuth setup
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
Execute the following /POST request to the token endpoint. This should be made within 30 seconds of the previous step.

>`{{netsuite-api}}`/services/rest/auth/oauth2/v1/token

The body of the request should be:
* x-www-form-urlencoded
* include the following values:
  
>`grant_type`=authorization_code&  
`redirect_uri`=https%3A%2F%2Fsharpsync.net%2Fcallback-oauth&  
`refresh_token`={refresh-token}


<hr />

## Setup restlet for uploading thumbnails (SuiteApi)

Steps required:

* (done) Install SuiteApi
* (done) Setup OAuth
* Setup SuiteApi (this step)
* Create a new thumbnails folder in NetSuite
* Setup the datasource to point to the new restlet

Updating thumbnails in NetSuite requires the usage of an external restlet. The restlet used was developed by Tim Dietrich and is freely available at https://suiteapi.com. This is optional. Without it no thumbnail uploads are possible.

SuiteApi is a set of functions which assists an authenticated user with uploads of files using the NetSuite REST api. File uploads are not supported natively, and this set of scripts extends the functionality.

If for some reason the website below is unavailable, a copy of the Suite API zip file can be found here: [SuiteAPI-v2022.1.zip](SuiteApi.v2022.1.zip)
Follow the steps in the SuiteApi setup 

* Navigate to latest version of  [SuiteAPI](https://suiteapi.com)
* [Download](https://tdietrich-opensource.s3.amazonaws.com/suitescripts/SuiteAPI-v2022.1.zip) the SuiteApi zip file for the restlet
* Install using the [instructions](https://suiteapi.com/documentation/) on the site <sup>**</sup>


** If the above link / website cannot be found, a copy (current at the time of writing) of the file and the instructions can be found using [this link](markdown/suite-api.md)


<hr />

## Setup an upload folder

**Goal**: To get a folder id

Steps required:

* (done) Install SuiteApi
* (done) Setup OAuth 
* (done) Setup SuiteApi 
* Create a new thumbnails folder in NetSuite (this step)
* Setup the datasource to point to the new restlet
 
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
  
Copy the value of the folderId and put it somewhere for later reference
 
## Putting it all together - Setup the datasource to point to the new restlet

With the copied URL in the previous step, and the `folderId` and `scriptId` in hand, it's time to setup the datasource in SharpSync. 

In SharpSync add a new data source > NetSuite.

### Configuring NetSuite

There are 2 configuration sections for each datasource
* Authentication
* BOM Configuration

#### Authentication

* Navigate to the Datasources > Config UI
* Select the NetSuite datasource > Add
* Set the server url > Click 'Update'
* Click the Ping button to test the connection. This is optional and will not work if ICMP is disabled on the server
* Click the 'Configure' button
* Enter the following values:
  
  | Name                | Description                                                                                                                                    | Recommended value                                                                 |
  | ------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------- |
  | Base API Path       | The location where data is pulled from                                                                                                         | https://{companyId}.suitetalk.api.netsuite.com                                    |
  | Authentication Type | Which authentication method you'd like to use to connect to NetSuite                                                                           | OAuth 2.0                                                                         |
  | OAuth Url           | The URL against which your OAuth authentication occurs                                                                                         | https://{companyId}.app.netsuite.com/app/login/oauth2/authorize.nl                |
  | OAuth Token Url     | The URL against which your OAuth token is refreshed                                                                                            | https://{companyId}.suitetalk.api.netsuite.com/services/rest/auth/oauth2/v1/token |
  | Client Id           | The client id generated by the integration record created                                                                                      | -                                                                                 |
  | Client Secret       | The client secrete generated by the integration record created                                                                                 | -                                                                                 |
  | OAuth Scopes        | The scopes required to get data. The `restlets` scope is optional but highly recommended. Without it you will not be able to upload thumbnails | rest_webservices,restlets                                                         |
  

#### BOM Configuration
  | Name                           | Description                                                                                                                               | Recommended value                                                                                                                                                                             |
  | ------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
  | Top level assembly column name | When querying the data you may use this value to identify assemblies (optional)                                                           | itemid                                                                                                                                                                                        |
  | SuiteQL BOM Query              | The query used to select data using SuiteQl                                                                                               | `SELECT ItemID, id, displayName FROM Item WHERE ItemID = '{uniquePartNumber}'`. Note that the place holder `{uniquePartNumber}` must stay as this is used to find items related to assemblies |
  | Servlet URL                    | The url of the servlet where thumbnails will be uploaded. Optional but recommented. If specified, include the `folderId` param at the end | https://{companyId}.restlets.api.netsuite.com/app/site/hosting/restlet.nl?script=2943&deploy=1&folderId={folderId}                                                                            |
  | Thumbnail column name          | The column to update in NetSuite using the file ID of the uploaded thumbnail                                                              | custitem_mycol_image                                                                                                                                                                          |
  

* Enter the URL of the restlet, followed by `&folderId=` and the id of the folder in the first steps
* Enter the folder ID into the UI in the form
 
> `{{netsuite-api}}`/app/site/hosting/restlet.nl?script={yourScriptId}&deploy=1&folderId={folderId}

e.g.

> `{{netsuite-api}}`/app/site/hosting/restlet.nl?script=`2743`&deploy=1&folderId=`19578359`


See also 

* [OAuth](../../authentication/markdown/oauth.md)
