# Setting up the Solidworks PDM Web 2



This documentation is a work in progress



There are the major components required:

* Static IP address OR DynDNS subscription for dynamic ip address resolution
* TLS Certificate
* Web2 API server
* Web2 PDM server (optional)

## Static IP or DynDNS

A static ip address means that an address for a machine (your pdm server) stays the same. If you don't own a static IP address (preferable), then a DynDNS update client is preferred.
Documentation on DynDNS clients can be found here [https://help.dyn.com/update-client-faqs/](https://help.dyn.com/update-client-faqs/)

A domain name points to a static ip address (your pdm server). A domain name is not strictly necessary but can be more convenient to use than an ip address.
A domain name is something that your company would use on the internet to host your own website at e.g.

> https://yourcompany.com.

## TLS Certificate

A TLS certificate is something that you use to encrypt the traffic between `https://yourcompany.com` and `https://app.sharpsync.net`. A TLS certificate is used to change the _type_ of traffic from `http` => `https`
A TLS certificate may be obtained from a certificate authority such as Digicert or GoDaddy

> [https://www.digicert.com/tls-ssl/compare-single-domain-certificates](https://www.digicert.com/tls-ssl/compare-single-domain-certificates)

OR 

> [https://www.godaddy.com/en-ca/web-security/ssl-certificate](https://www.godaddy.com/en-ca/web-security/ssl-certificate)

For the more adventurous amongst you there are free TLS certificates available from Let's encrypt, there processes may be reviewed here

## SW PDM Web2 API Server
### Installing the WebAPI server

 - [ ] [todo]

## Installing theWeb2 PDM Server (Optional)
- [ ] [todo]
   
