# Propel

<em>This document is a work in progress</em>

Propel is a cloud ERP available from salesforce. Please also see [(https://www.propelsoftware.com/)](https://www.propelsoftware.com/)

To configure a Propel intance you need:
* The base API path of your Propel cloud instance which is of the form: `https://{propel-instance}.my.salesforce.com`
* Propel uses the OAuth 2.0 protocol to authenticate, therefore, a code grant url, a refresh token url and the oauth scopes need to be supplied, they are of the form:
    * Code Grant URL: `https://{propel-instance}.my.salesforce.com/services/oauth2/authorize`
    * Refresh Token URL: `https://{propel-instance}.my.salesforce.com/services/oauth2/token`
    * Scopes: `full api web refresh_token offline_access`

## Setup Propel Datasource

* Login on the application
* Navigate to `Data Sources`
* On the right > Select Propel > Add
* Click the configure button
* On the first tab, enter the OAuth credentials
* On the second tab (BOM Configuration), select the preferred Bom children selection option
* Click the `Save` button
* Click the `Authenticate` button

## Setup Propel Property Mappings

* Navigate to `Property Mapping`
* After creating/adding your property mappings from your primary/CAD source, select the corresponding Propel property from the drop down selection boxes.

## Notes:

In the current implementation of the SharpSync Propel Module:
* New Propel items are are already created with at least a Name and Category prior to exporting to SharpSync.
* Existing Propel item Names or Part Numbers (Propel property name: `"Name"`) cannot be edited.
* Existing Propel item Categories (Propel property name: `"PDLM__Category__c"`) cannot be edited.
