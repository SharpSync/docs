# NetSuite Setup of Thumbnail foler
    
**Goal**: To get a folder id to use as the `folderId` in the thumbnail setup
 
* Navigate to NetSuite
* Click on the `Documents` menu item
* Click on the `Files` sub menu item > File Cabinet
* Click on the `New Folder` button
  * Folder name: `SharpSync`
  * Subfolder of: nothing
  * Type `Documents and Files`
  * Click `Save`
* Click on the `New Folder` button again
  * Folder name: `Thumbnails`
  * Subfolder of: `SharpSync`
  * Type `Documents and Files`
  * Click `Save`

With this last folder selected in the file cabinet, take note of the folder id in the URL. This will be used later. The url at the top will look something like this:

> https://`{companyId}`.app.netsuite.com/app/common/media/mediaitemfolders.nl?`folder=20149768`&whence=&cmid=...
  
Copy the value of the folderId and put it somewhere for later reference
   
See also 

* [OAuth](../../authentication/markdown/oauth.md)
