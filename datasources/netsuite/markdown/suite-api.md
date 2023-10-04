# SuiteAPI Overview

If possible always use the original source. A clone of the opensource suitescript is made here for reference. All credits to [Tim Dietrich](https://timdietrich.me/) for the original work.

## Original source:  [https://suiteapi.com/](https://suiteapi.com/)
SuiteAPI is an open source, alternative Web API for the NetSuite platform. It makes it easy for developers to integrate with NetSuite, regardless of the type of application that they're developing or the technology they're developing it with.

With SuiteAPI, developers can:
• Retrieve records.
• Get SuiteQL query results.
• Access the results of saved searches.
• Upload and download files to and from the file cabinet.
• Send email messages via NetSuite.
• Generate PDFs based on transactions or ad-hoc XML code.
• And more.

In addition, SuiteAPI can be extended to add support for working with transactions (such as sales orders, purchase orders, quotes, etc), entities (such as customers, vendors, employees, etc), items, custom records, custom lists, and more.

Unlike NetSuite's SuiteTalk REST Web service, SuiteAPI isn't RESTful. SuiteAPI is more of an RPC-style (short for "remote procedure call") Web API. All requests are made as HTTP POSTs, with JSON-encoded payloads. The response payloads are also JSON-encoded.

SuiteAPI is very easy to use, it's reliable, and it's secure (it uses NetSuite's native security model, including roles, tokens, etc). It also has a very small footprint, consisting of a single RESTlet.

To get started with SuiteAPI, you can [download](https://suiteapi.com/download/) it here and learn how to [install and configure it here](https://suiteapi.com/install/). For information about the procedure that SuiteAPI supports, the [documentation](https://suiteapi.com/documentation/) is available here.

> NOTE: If for some reason the original source is unavailable, a copy of the Suite API zip file can be found here: [SuiteAPI-v2022.1.zip](../resources/SuiteApi.v2022.1.zip)

## Step: Installation

After downloading the .zip file, upload SuiteAPI to Your NetSuite Account
If you haven't already logged into your NetSuite account, do that now. I highly recommend that you first install SuiteAPI into a sandbox account for testing before installing it into a production account. And be sure to login as an administrator.

Next, navigate to the account's File Cabinet, and specifically to the SuiteScripts folder. Documents > Files > SuiteScripts.

Add a subfolder for SuiteAPI. Again, navigate to the SuiteScripts folder in the File Cabinet. Then click the "New Folder" button in the header. For the Folder Name, enter: SuiteAPI. You can leave all of the other fields as they are. Click the Save button to create the folder.

Now we'll upload the SuiteAPI SuiteScript file to the folder that you created. In the File Cabinet, you should be in the SuiteScripts > SuiteAPI folder. If not, navigate to it. Then click the "Add File" button in the header. Then navigate to the location of the file that you unzipped earlier. The file that you want to select is named: suiteapi.restlet.js

The script file is very small, and should upload quickly. When the file has been uploaded, you'll see it listed in the SuiteScripts > SuiteAPI folder

## Step: Create Script and Script Deployment Records
Next, we'll create a Script Record for SuiteAPI.

Navigate to: Customization > Scripting > Scripts > New

The "Upload Script File" form will appear. In the Script File field, enter: suiteapi The field will auto-complete, and you'll see the file that you uploaded ("suiteapi.restlet.js") listed. Select it, and then click the "Create Script Record" button.

The "Script" form will appear. Enter the following values into the form:
• Name: SuiteAPI
• ID: _suiteapi
• Description: An alternative Web API for the NetSuite platform.

Click on the Deployments tab, and set these values in the first row:
• Title: SuiteAPI
• ID: _suiteapi

Make sure that the Deployed checkbox is checked, and set the Status to Released.

Click the Save button.

The Script and Script Deployment records will be created, and the Script record will be displayed.

Click on the Deployments tab, and click on the title ("SuiteAPI") of the deployment that is displayed. This will load the Script Deployment.

Copy the value of the External URL that is displayed. It will be something like:
https://99999999.restlets.api.netsuite.com/app/site/hosting/restlet.nl?script=925&deploy=1


### Roles

It is highly recommend creating one (or more) custom roles for use with SuiteAPI. These roles will be used to specify the NetSuite resources that your SuiteAPI-based integrations will have access to, and the type of permissions that they'll have. For example, you might create a role designed specifically for querying item information, and another that has the ability to create and/or update transactions.

See the documentation for more information about creating custom roles [here](https://suiteapi.com/install).