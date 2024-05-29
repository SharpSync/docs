# Errors in Production

*  [Concurrency limits](#concurrency-limits)
*  [Thumbnail uploads fail with errors](#thumbnail-uploads-fail-with-errors)

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
