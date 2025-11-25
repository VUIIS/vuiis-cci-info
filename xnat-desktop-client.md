# Using the XNAT Desktop Client with VUIIS CCI XNAT

https://www.xnat.org/download/desktop-client/

The XNAT Desktop Client provides a graphical interface for bulk uploads and downloads. It may not support
downloading our custom assessors - this has not been tested - but it will certainly work for uploads.

If using it for uploads, it's critical not to open multiple sessions or connections, to avoid crashing the
XNAT receive process.

So, if using it, adjust the connection settings to reduce the default simultaneous transfers from 6 to 1:

1. Log in to the XNAT server
2. Go to settings via gear icon
3. Under the "User Settings" tab, look for "Upload Concurrency" and set to 1.
