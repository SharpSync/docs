# Onshape Setup

Onshape setup is quite easy.

* Select + Add the Onshape datasource
* Configure the authentication options
* Click Authenticate
  
## Step: Configure the authentication options

* Click the configure button
* For Onshape Professional or the free version:
* ![Onshape setup](../images/onshape-oauth-config.png)
* For enterprise environments, fill in the values for your enterprise name. This means that in the url, instead of
  
> `https://cad.onshape.com/api` 

you will have

> `https://{enterpriseName}.onshape.com/api`


## Troubleshooting

### Cannot pull Onshape BOM
The following response in the network tab with a 502  statuscode
```json
{
    "message": "Could not pull the bom from Onshape - request was Forbidden. Check that the document hostname/origin matches the datasource server hostname"
}
```
Let's say the enterprise name is `starkindustries.onshape.com` .

Check:
- The hostname is configured correctly in the datasource (e.g. cad.onshape.com vs starkindustries.onshape.com)
- The oauth hostnames all match 
	- For free version: `oauth.onshape.com` and NOT `cad.onshape.com`
	- For enterprise version `starkindustries.onshape.com` and NOT `oauth.onshape.com`