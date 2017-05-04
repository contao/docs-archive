# Frequently Asked Questions

## Error *broken SHA1 signature*

If you get a message similar to the following after uploading the
Contao Manager to your server, the file was most likely not uploaded
correctly. Make sure to use binary transfer mode if upload the file
using an FTP connection.

```
Fatal error: Uncaught exception 'PharException' with message 'phar 
"…/contao-manager.phar.php" SHA1 signature could not be verified: 
broken signature' in …/contao-manager.phar.php …
```
