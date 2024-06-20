# Propel

<em>This document is a work in progress</em>

Propel is a cloud ERP available from salesforce. Please also see [(https://www.propelsoftware.com/)](https://www.propelsoftware.com/)

To configure a Propel intance you need:
* The base API path of your Propel cloud instance which is of the form: `https://{propel-instance}.my.salesforce.com/services`
* Propel uses the OAuth 2.0 protocol to authenticate, therefore, a code grant url, a refresh token url and the oauth scopes need to be supplied, they are of the form:
    * Code Grant URL: `https://{propel-instance}.my.salesforce.com/services/oauth2/authorize`
    * Refresh Token URL: `https://{propel-instance}.my.salesforce.com/services/oauth2/token`
    * Scopes: `full api web refresh_token offline_access`

## Setup steps

* Login on the application
* Navigate to data sources
* On the right > Select Propel > Add
* Click the configure button
* On the first tab, enter the OAuth credentials
* On the second tab (BOM Configuration)
* Click the `Save` button
* Click the `Authenticate` button

