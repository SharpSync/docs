# Errors in Production

*  [Concurrency limits](#concurrency-limits)
*  [Thumbnail uploads fail with errors](#thumbnail-uploads-fail-with-errors)
*  [Error running script](#error-running-script)
*  [Cannot update BOMs using incompatible subsidiaries](#current-limitation-cannot-update-bom-rows-with-incompatible-subsidiaries)

## Concurrency limits.

In NetSuite you can review the concurrency limits and the performance of a RESTlet using the `Setup > Other Setup > Integration Governance` section.
Concurrency of requests are monitored in NetSuite and may be subject to rejection if the limit is exceeded

or 

> https://{your-account-id}.app.netsuite.com/app/webservices/governance/governance.nl?whence=

* Account Concurrency limit - Specific account limit based on service tier and license count
* Peak concurrency - Max requests received in 1 moment in the last 30 days
* Rejected requests - Requests exceeding the concurrency limit in the last 30 days
* Total Requests - Number of requests for restlets and services in the last 30 days.
* Rejected Requests Ratio - Ratio of rejected requests - if it exceeds 1% then concurrency might be the root cause

Sometimes you may see that requests fail with a result of `Unauthorized`. This happens when the concurrency limit is exceeded.

## Thumbnail uploads fail with errors
> Failed to update document thumbnail for bomPart, (errorDetails follow...)

This is typically because the user permissions is insufficient to upload document thumbnails to the specified cabinet location in NetSuite.

This message is also typically followed by
>Invalid login attempt. For more details, see the Login Audit Trail in the NetSuite UI at Setup > Users/Roles > User Management > View Login Audit Trail.

## Error running script

Should you get the below error despite the fact that the code is correct, make sure the the name of the script file has a `.js` at the end

```javascript
{
    "error": {
        "code": "MODULE_DOES_NOT_EXIST",
        "message": "{\"type\":\"error.SuiteScriptModuleLoaderError\",\"name\":\"MODULE_DOES_NOT_EXIST\",\"message\":\"Module does not exist: /SuiteScripts/SharpSync/sharpsync-item-create.js\",\"stack\":[]}"
    }
}
```

## Current limitation: Cannot update bom rows with incompatible subsidiaries

At the time of writing there is a limitation for advanced BOMs. The limitation only occurs when the subsidiary is incompatible with another subsidiary. To fix the issue:

* All commponents (parts / assemblies) added to a BOM revision must have a compatible subsidiary as the inventory item (e.g. AssemblyItem / NonInventorResaleItem)
* If it does not - you may see an error in the logs stating something along the lines of
  > Error while accessing a resource. You have entered an Invalid Field Value 18099 for the following field: item.
* If this is the case, locate the item using its Id e.g.
> https://[customerId].app.netsuite.com/app/common/item/item.nl?id=18099
* Make sure that the subsidiary matches that of the Bom to which it is being added.
