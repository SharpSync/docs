# Netsuite Setup

Updating thumbnails in Netsuite requires the usage of an external restlet. The restlet used was developed by Tim Dietrich and is freely available at https://suiteapi.com

Steps required:
* Navigate to latest version of [SuiteApi](SuiteAPI-v2022.1)
* [Download](https://tdietrich-opensource.s3.amazonaws.com/suitescripts/SuiteAPI-v2022.1.zip) the SuiteApi zip file for the restlet
* Install using the [instructions](https://suiteapi.com/documentation/) on the site <sup>**</sup>


** At the time of writing the documentation was available. If the above link / website cannot be found, an older copy of the file and the instructions can be found using the links below:


## File
Suite API zip file [SuiteAPI-v2022.1.zip](SuiteApi.v2022.1.zip)

## Instructions
 SuiteAPI Documentation
All SuiteAPI requests are sent using the HTTP POST method, and both the request and response payloads are JSON-encoded.

Requests include the name of the procedure that is to be run, and any required and optional parameters, depending on the procedure being called.

For example, to call SuiteAPI's recordGet procedure, the request would look like this:
```json
{
  "procedure": "recordGet",
  "type": "salesorder",
  "id": 26049
}
```
When sending a request, set the HTTP "Content-Type" header to: application/json

When using token-based authentication, the HTTP "Authorization" header should be a valid OAuth 1.0a Authorization Header.

Unless a fatal error occurs, the HTTP response code returned by SuiteAPI will always be 200 OK. Error information will be returned in the response body.

The table below lists all of the standard procedures that SuiteAPI supports based on the most recent release.

## Configuration

## Create a folder
* Create a new folder in NetSuite file cabinet
* Navigate to the list of folders
* Get the ID of the folder
* Enter the folder ID into the UI in the form
 
> `{{netsuite-api}}`/app/site/hosting/restlet.nl?script=[yourScriptId]&deploy=1&folderId=[folderId]

e.g.

> {{netsuite-api}}/app/site/hosting/restlet.nl?script=2943&deploy=1&folderId=19575359