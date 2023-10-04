# SuiteAPI Overview

If possible always use the original source. A clone of the opensource suitescript is made here for reference. All credits to [Tim Dietrich](https://timdietrich.me/) for the original work.

## Original source:  [https://suiteapi.com/](https://suiteapi.com/)
SuiteAPI is an open source, alternative Web API for the NetSuite platform. It makes it easy for developers to integrate with NetSuite, regardless of the type of application that they're developing or the technology they're developing it with.

 
* Extract the contents of the downloaded zip file
* In NetSuite Navigate to `Documents` > `Files` > `File Cabinet`, <span style="color:orange">select the system folder called `SuiteScripts`</span>
* Click on the `New Folder` button again
  * Folder name: `SharpSync`
  * Subfolder of: `SuiteScripts`
  * Type `Documents and Files`
  * Click `Save`
* With the `SharpSync` folder selected in NetSuite, click `Add file`
* Select the extracted `suiteapi.restlet.js` file  
  
### Step: Create script deployment record
* Navigate to `Setup` > `Customization` > `Scripts` > `New`
* In the Script file entry, enter `suiteapi.restlet.js` 
* Click `Create Script Record`
* On the new form enter the values:
  * Name: `SharpSyncSuiteAPI`
  * ID: `_sharpsync_suite_api`
  * Description: `Restlet for uploading files and thumbnails for SharpSync`
* Click on the `Deployments` tab at the bottom and in the first row set
  * Title: `SharpSyncSuiteAPI`
  * ID: `_sharpsync_suite_api`
* IMPORTANT: Confirm that in the Deployed Column it reads Yes
* Change the `Status` from `Testing` > `Released`
* Click `Save`
* Click the Deployments tab
* Click on the title of the deployment (SharpSyncSuiteAPI)
* Copy the External URL. It will look something like this:
* https://{companyId}.restlets.api.netsuite.com/app/site/hosting/restlet.nl?script=925&deploy=1

### To get back to this page:
* Navigate to `Setup` > `Customization` > `Scripts`
* Search for and select `SharpSyncSuiteApi`
* Click the View link
* On the deployments tab, click the title of the deployment
* The external URL will be available
  
Copy the value of the External URL that is displayed. It will be something like:
https://99999999.restlets.api.netsuite.com/app/site/hosting/restlet.nl?script=925&deploy=1


### Roles

It is highly recommend creating one (or more) custom roles for use with SuiteAPI. These roles will be used to specify the NetSuite resources that your SuiteAPI-based integrations will have access to, and the type of permissions that they'll have. For example, you might create a role designed specifically for querying item information, and another that has the ability to create and/or update transactions.

See the documentation for more information about creating custom roles [here](https://suiteapi.com/install).