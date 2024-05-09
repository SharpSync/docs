# Microsoft Dynamics 365

## Terms

The terms below is use to describe how to interrogate MS Dynamics for data

* Tenant: A tenant is an organization or directory.
* Application: A unique application that belongs to a tenant and has a unique ID (guid)
* Company: A tenant may have multiple companies (e.g. an organization may trade as different company names in different regions)
* Items: An item is created in a company and is queried using the company id

> /GET businesscentralprefix/companies({id})/items({id})

[In progress]
