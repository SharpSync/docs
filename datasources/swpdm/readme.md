# SOLIDWORKS PDM  
Solidworks PDM is a data management solution from Dassault Systemes. It allows you to manage Solidworks files and their revisions, along with metadata like Vendor, Material, Description, etc.

## Prerequisites
* The PDM Profession version must be used
* The PDM Professional version API must be exposed to the internet using the Web API setup guide

## Installing the addin

### Extracting the files
When downloading the client from the `Downloads` section, a new zip file will be created on your machine.
Extract the files to a convenient location using `Right click > Extract all...`

### Preparing the files for installation

By default Windows will block all `.dll` and `.exe` files downloaded from an internet source. Because of this the addin will fail to install. You first need to unblock it. To unblock a file:

* `Right Click > Properties` 
* At the bottom of the first tab, There is a warninig
* Select the checkbox reading `Unblock`
* Click the apply button
* Repeat for all other files in the folder

![images/windows_blocked_addin.png](images/windows_blocked_addin.png)

### Next steps: See [setup](markdown/swxpdm-setup.md)
