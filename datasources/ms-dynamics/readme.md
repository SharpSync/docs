# Dynamics 365 Business Central

<em>This document is a work in progress</em>

Dynamics 365 Business Central is a cloud ERP available from Microsoft. Please also see [(https://www.microsoft.com/en-us/dynamics-365/products/business-central)

To configure a Dynamics 365 Business Central datasource instance you need:
* The base API path of Dynamics 365 Business Central cloud which is: `https://api.businesscentral.dynamics.com`
* Dynamics 365 Business Central uses the OAuth 2.0 protocol to authenticate, therefore, a code grant url, a refresh token url and the oauth scopes need to be supplied, they are of the form:
    * Code Grant URL: `https://login.microsoftonline.com/{{sharpsync-app-tenant-id}}/oauth2/v2.0/authorize`
    * Refresh Token URL: `https://login.microsoftonline.com/{{sharpsync-app-tenant-id}}/oauth2/v2.0/token`
    * Scopes: `https://api.businesscentral.dynamics.com/.default offline_access`
* Your Dynamics 365 Business Central instance company id and environment:
    * The company id can be obtained by following these steps from your Dynamics 365 Business Central instance web interface:
      * Log in to your Business Central account and navigate to the Companies tab.
      * Select the company you want to use.
      * Click the question mark button on the top right corner and select Help & Support.
      * Under the troubleshooting section, click Inspect pages and data.
      * In the inspector, you can enter Id in the search field and the first result contains your company ID.
      * Id (8000, GUID) or $systemId (2000000000, GUID)
    * The company environment is usually visible on the top right of your Dynamics 365 Business Central instance web interface.
      * The environment is usually `Production` or `Sandbox`
* All the above credentials (except for your instance's company id and environment) will already be set in SharpSync when you are configuring your data source.
    

## Setup Dynamics 365 Business Central Datasource

* Login on the application
* Navigate to `Data Sources`
* On the right > Select Dynamics365 > Add
* Click the configure button
* On the first tab `Authentication`, select the `OAuth 2.0` authentication type
* On the second tab `Configuration`, enter your Company Id and Environment as described in the previous section
* Click the `Save` button
* Click the `Authenticate` button

## Setup Dynamics 365 Business Central Property Mappings

* Navigate to `Property Mapping`
* After creating/adding your property mappings from your primary/CAD source, select the corresponding Propel property from the drop down selection boxes.

## Definitions

Dynamics 365 Business Central API selected definitions:

* Tenant: A tenant is an organization or directory.
* Application: A unique application that belongs to a tenant and has a unique ID (guid)
* Company: A tenant may have multiple companies (e.g. an organization may trade as different company names in different regions)
* Items: An item is created in a company and is queried using the company id

## Notes:

In the current implementation of the Dynamics 365 Business Central Module:


[In progress]

